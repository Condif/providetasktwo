<template>
  <form @submit.prevent="submit" style="width: 20rem">
    <div class="form-group">
      <label class="form__label">Förnamn</label>
      <input class="form__input" v-model.trim="$v.firstName.$model" />
    </div>
    <div class="error" v-if="!$v.firstName.required">Obligatoriskt fält</div>
    <div class="error" v-if="!$v.firstName.minLength">
      Förnamnet måste innehålla minst
      {{ $v.firstName.$params.minLength.min }} bokstäver.
    </div>
    <div
      class="form-group"
      :class="{ 'form-group-error': $v.firstName.$error }"
    >
      <label class="form__label">Efternamn</label>
      <input class="form__input" v-model.trim="$v.lastName.$model" />
    </div>
    <div class="error" v-if="!$v.lastName.required">Obligatoriskt fält</div>
    <div class="error" v-if="!$v.lastName.minLength">
      Efternamnet måste innehålla minst
      {{ $v.lastName.$params.minLength.min }} bokstäver.
    </div>
    <div class="form-group" :class="{ 'form-group-error': $v.email.$error }">
      <label class="form__label">Email</label>
      <input class="form__input" v-model.trim="$v.email.$model" />
    </div>
    <div class="error" v-if="!$v.email.required">Obligatoriskt fält</div>
    <div class="error" v-if="!$v.email.minLength">
      Emailen måste innehålla minst
      {{ $v.email.$params.minLength.min }} bokstäver.
    </div>
    <div class="buttonDiv">
      <button
        class="button"
        type="submit"
        :disabled="submitStatus === 'PENDING'"
      >
        Betala
      </button>
      <p class="typo__p" v-if="submitStatus === 'OK'">
        Tack för ditt köp!
      </p>
      <p class="typo__p" v-if="submitStatus === 'ERROR'">
        Var snäll och fyll i uppgifterna korrekt.
      </p>
      <p class="typo__p" v-if="submitStatus === 'PENDING'">Skickas...</p>
    </div>
  </form>
</template>
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
<script>
// import BaseButton from "@/components/BaseButton";
import { validationMixin } from "vuelidate";
import { required, minLength } from "vuelidate/lib/validators";
import axios from "axios";
const url = "https://ftest.dev3.provideit.se";
const productEndpoint = "/wp-json/wc/v3/orders";
// const keys =
  // "consumer_key=ck_9b6f2b633c777a37bccb7553cf8b1d47c7e3447c&consumer_secret=cs_55cfbde055597f2eb86077159500e65f1423ac7e";
export default {
  mixins: [validationMixin],
  validations: {
    firstName: {
      required,
      minLength: minLength(4),
    },
    lastName: {
      required,
      minLength: minLength(4),
    },
    email: {
      required,
      minLength: minLength(4),
    },
  },
  props: {
    placeOrder: { type: Function },
    cartList: { type: Array },
  },
  data() {
    return {
      firstName: "",
      lastName: "",
      email: "",
      submitStatus: null,
    };
  },
  methods: {
    submit() {
       let newOrder = new FormData;
      newOrder = {
        billing: {},
        line_items: [],
      };
      newOrder["billing"] = {
        first_name: this.firstName,
        last_name: this.lastName,
        email: this.email,
      };
      this.cartList.forEach((product) => {
        newOrder.line_items.push({["product_id"]: product.id, ["quantity"]:  (product.grouped_products.length + 1)});
      });
      this.$v.$touch();
      if (this.$v.$invalid) {
        this.submitStatus = "ERROR";
      } else {
        axios({
          method: "post",
          auth: {
            username: "ck_9b6f2b633c777a37bccb7553cf8b1d47c7e3447c",
            password: "cs_55cfbde055597f2eb86077159500e65f1423ac7e"
          },
          headers: {
            "Content-Type": "application/json",
            "Accept": "application/json"
          },
          url: url + productEndpoint,
          data: JSON.stringify(newOrder),
        })
          .catch((err) => console.log(err));
        this.submitStatus = "PENDING";
        setTimeout(() => {
          this.submitStatus = "OK";
          this.$emit("newOrder", newOrder);
          this.$router.push("/receipt")
        }, 500);
      }
    },
  },
};
</script>

<style scoped></style>
