<template>
  <div class="myPages">
    <h1 class="header">Mina sidor</h1>
    <BaseCard class="baseCard">
      <div class="personalInfo">
        <div class="fullName">
          <h4 class="margin">Förnamn:{{userInfo.firstName}} </h4>
        </div>
        <div class="fullName">
          <h4 class="margin">Efternamn:</h4>
        </div>
        <div class="email">
          <h4 class="margin">Email:</h4>
        </div>
        <div class="id">
          <h4 class="margin">Id: {{loginInfo.id}} </h4>
        </div>
      </div>
    </BaseCard>
  </div>
</template>

<script>
import BaseCard from "@/components/BaseCard";
export default {
  components: {
    BaseCard,
  },
  props: ["loginInfo", "userInfo"]
};
</script>

<style scoped>
.baseCard {
  width: 50rem;
}

.margin {
  margin: 1rem;
}
.fullName {
  display: flex;
}
.header {
    text-align: center;
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
