<template>
  <div class="login">
      <h1 style="textAlign: center;">Logga in</h1>
    <BaseCard class="container">
      <form @submit.prevent="submit" style="width: 20rem">
        <div
          class="form-group"
          :class="{ 'form-group-error': $v.email.$error }"
        >
          <label class="form__label">Email</label>
          <input class="form__input" v-model.trim="$v.email.$model" />
        </div>
        <div class="error" v-if="!$v.email.email">Detta måste vara en email</div>
        <div class="error" v-if="!$v.email.required">Obligatoriskt fält, angiven email är ditt användarnamn</div>
        <div class="error" v-if="!$v.email.minLength">
          Emailen måste innehålla minst
          {{ $v.email.$params.minLength.min }} bokstäver.
        </div>
        <div
          class="form-group"
          :class="{ 'form-group-error': $v.password.$error }"
        >
          <label class="form__label" >Lösenord</label>
          <input class="form__input" type="password" v-model.trim="$v.password.$model" />
        </div>
        <div class="error" v-if="!$v.password.required">Obligatoriskt fält</div>
        <div class="error" v-if="!$v.password.minLength">
          Lösenordet måste innehålla minst
          {{ $v.password.$params.minLength.min }} tecken.
        </div>
        <div class="buttonDiv">
          <button
            class="button"
            type="submit"
            :disabled="submitStatus === 'PENDING'"
          >
            Logga in
          </button>
          <p class="typo__p" v-if="submitStatus === 'OK'">
            Du är inloggad!
          </p>
          <p class="typo__p" v-if="submitStatus === 'ERROR'">
            Var snäll och fyll i uppgifterna korrekt.
          </p>
          <p class="typo__p" v-if="submitStatus === 'PENDING'">Skickas...</p>
        </div>
      </form>
    </BaseCard>
  </div>
</template>

<script>
import { validationMixin } from "vuelidate";
import { required, minLength, email } from "vuelidate/lib/validators";
import axios from "axios";
import BaseCard from "@/components/BaseCard";
const url = "https://ftest.dev3.provideit.se";
const loginEndpoint = "/wp-json/custom/login";
export default {
  mixins: [validationMixin],
  data() {
    return {
    //   firstName: "",
    //   lastName: "",
      email: "",
      password: "",
      submitStatus: null,
    };
  },
  validations: {
    // firstName: {
    //   required,
    //   minLength: minLength(4),
    // },
    // lastName: {
    //   required,  
    //   minLength: minLength(4),
    // },
    email: {
      required,
      email,
      minLength: minLength(4),
    },
    password: {
        required,
        minLength: minLength(4),
    }
  },
  components: {
    BaseCard,
  },
  methods: {
    submit() {

    let params = new FormData();
      params.append('password', this.password);
      params.append('username', this.email);
      this.$v.$touch();
      if (this.$v.$invalid) {
        this.submitStatus = "ERROR";
      } else {
        axios({
          method: "post",
          url: url + loginEndpoint,
          data: params,
        })
          .then((res) => {
            console.log(res);
            this.$emit("login", res.data);
            this.$router.push("/");
          })
          .catch((err) => console.log(err));
        this.submitStatus = "PENDING";
        setTimeout(() => {
          this.submitStatus = "OK";
        }, 500);
      }
    },
  },
};
</script>

<style scoped>
.form-group {
  margin-top: 1rem;
  display: flex;
  flex-direction: column;
}

.form__input {
  border-radius: 0.2rem;
}

.error {
  color: pink;
  padding: 0.2rem;
}
.buttonDiv {
  display: flex;
  align-items: center;
  flex-direction: column;
}
.button {
  margin: 0.5rem;
  border: none;
  color: white;
  padding: 0.8rem;
  border-radius: 1rem;
  background: rgb(109, 216, 83);
  cursor: pointer;
  width: 8rem;
}
</style>
