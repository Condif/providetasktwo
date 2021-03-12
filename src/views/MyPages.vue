<template>
  <div class="myPages">
    <h1 class="header">Mina sidor</h1>
    <BaseCard
      class="baseCard"
      v-if="loginInfo && loginInfo.user && loginInfo.user.ID"
    >
      <form style="width: 20rem">
        <div class="fulldisplay_name">
          <div class="form-group"></div>

          <h4 class="margin">Namn:{{ loginInfo.user.data.display_name }}</h4>
          <span
            @click="
              enableEditing(loginInfo.user.data.display_name, 'display_name')
            "
            class="material-icons"
          >
            mode
          </span>
        </div>

        <div v-if="display_name">
          <input v-model="tempValuedisplay_name" class="input" />
          <BaseButton
            padding="0.4rem"
            background="pink"
            style="margin: 0.3rem;"
            @onClick="disableEditing('display_name')"
            >Avbryt</BaseButton
          >
          <BaseButton
            padding="0.4rem"
            style="margin: 0.3rem;"
            @onClick="saveEdit('display_name')"
            >Spara</BaseButton
          >
          <div class="error" v-if="!$v.tempValuedisplay_name.required">
            Obligatoriskt fält
          </div>
          <div class="error" v-if="!$v.tempValuedisplay_name.minLength">
            Förnamnet måste innehålla minst
            {{ $v.tempValuedisplay_name.$params.minLength.min }} bokstäver.
          </div>
        </div>
        <div class="email">
          <h4 class="margin">Email: {{ loginInfo.user.data.user_email }}</h4>
          <span
            class="material-icons"
            @click="enableEditing(loginInfo.user.data.user_email, 'Email')"
            >mode</span
          >
        </div>
        <div v-if="Email">
          <div
            class="form-group"
            :class="{ 'form-group-error': $v.tempValueEmail.$error }"
          >
            <input v-model="tempValueEmail" class="input" />
            <BaseButton
              padding="0.4rem"
              background="pink"
              style="margin: 0.3rem;"
              @onClick="disableEditing('Email')"
              >Avbryt</BaseButton
            >
            <BaseButton
              padding="0.4rem"
              style="margin: 0.3rem;"
              @onClick="saveEdit('Email')"
              >Spara</BaseButton
            >
            <div class="error" v-if="!$v.tempValueEmail.email">
              Detta måste vara en email
            </div>
            <div class="error" v-if="!$v.tempValueEmail.required">
              Obligatoriskt fält
            </div>
            <div class="error" v-if="!$v.tempValueEmail.minLength">
              Emailen måste innehålla minst
              {{ $v.tempValueEmail.$params.minLength.min }} bokstäver.
            </div>
          </div>
        </div>
      </form>
    </BaseCard>
  </div>
</template>

<script>
import BaseCard from "@/components/BaseCard";
import BaseButton from "@/components/BaseButton";
import { validationMixin } from "vuelidate";
import { required, minLength, email } from "vuelidate/lib/validators";
// import axios from "axios";
// const url = "https://ftest.dev3.provideit.se/";
// const userEndpoint = "wp-json/wp/v2/users/";
export default {
  components: {
    BaseCard,
    BaseButton,
  },
  mixins: [validationMixin],
  validations: {
    tempValuedisplay_name: {
      required,
      minLength: minLength(4),
    },
    tempValueEmail: {
      required,
      email,
      minLength: minLength(4),
    },
  },
  data() {
    return {
      tempValuedisplay_name: null,
      tempValueEmail: null,
      display_name: false,
      Email: false,
      // submitStatus: null,
    };
  },
  props: ["loginInfo"],
  methods: {
    enableEditing: function(value, anchor) {
      this["tempValue" + anchor] = value;
      this[anchor] = true;
    },
    disableEditing: function(anchor) {
      this["tempValue" + anchor] = null;
      this[anchor] = false;
    },
    saveEdit: function(anchor) {
      let params = new FormData();
      params.append(anchor, this["tempValue" + anchor]);
      console.log(this.loginInfo.nonce);
      console.log(this["tempValue" + anchor]);
      console.log(anchor);
      let newNonce = this.loginInfo.nonce.replace(/^\s+/g, "");
      console.log(newNonce);
    
      // axios({
      //   method: "post",
      //   headers: {
      //     "X-WP-Nonce": newNonce,
      //     "Content-Type": "application/json",
      //     Accept: "application/json",
      //   },
      //   url: url + userEndpoint + this.loginInfo.user.ID,
      //   data: params,
      // })
      //   .then((res) => {
      //     console.log(res);
      //     console.log(this["tempValue" + anchor]);
      //     this["tempValue" + anchor];
      //     this.disableEditing();
      //   })
      //   .catch((err) => console.log(err));
    },
  },
};
</script>

<style scoped>
input {
  padding: 0.2rem;
  border-radius: 0.3rem;
  margin-right: 0.3rem;
}

.baseCard {
  width: 50rem;
}

.margin {
  margin: 1rem;
}
.fulldisplay_name,
.email {
  display: flex;
  place-items: center;
}
.header {
  text-align: center;
}
.material-icons {
  cursor: pointer;
  color: green;
}
@media screen and (max-width: 510px) {
  .baseCard {
    width: 20rem;
  }
}

@media screen and (min-width: 510px) and (max-width: 890px) {
  .baseCard {
    width: 30rem;
  }
}
@media screen and (min-width: 890px) and (max-width: 1400px) {
  .baseCard {
    width: 40rem;
  }
}
</style>
