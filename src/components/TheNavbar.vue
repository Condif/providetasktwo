<template>
  <div id="nav">
    <div class="links" style="color: white;">
        <router-link  to="/" exact>Hem</router-link> |
        <router-link  to="/about">Om</router-link> |
        <router-link  to="/mypages">Mina sidor</router-link>
    </div>
    <!-- v-if="this.$route.name !== 'Checkout' && this.$route.name !== 'Receipt' && this.$route.name !== 'Login'" -->
    <div  class="cart end" @click="$emit('open')" >
      <span class="material-icons" style="color:green;">
        shopping_cart
      </span>
    </div>
    <div class="login end"  >
      <router-link v-if="loginInfo && !loginInfo.user" to="login">Logga in</router-link>
    </div>
    <div class="login end" v-if="this.$route.name !== 'Login' && loginInfo && loginInfo.user && loginInfo.user.ID">
      <router-link to="login">Logga ut</router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "Navbar",
  props: ["loginInfo"]
};
</script>

<style scoped>
#nav {
  display: grid;
  grid-template-rows: repeat(12, 1fr);
  grid-column: 1 / 4;
  height: 5rem;
  width: 100%;
  background: rgb(51,51,51);
  align-items: center;
  opacity: 90%;
  position: fixed;
  
}
.links {
    grid-column: 7/13;
    grid-row: 2/10;
    margin-top: 1rem;
}

#nav a {
  font-weight: bold;
  color: white;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

.end {
    
    grid-row: 4/10;
    cursor: pointer;
    
}
.login {
  grid-column: 12/13;
}
.cart {
  grid-column: 11/13;
}

@media screen and (max-width: 570px) {
  .cart {
    grid-column: 2/13;
  }
  .login {
    grid-column: 13/13;
  }
  .links {
    grid-column: 7/13;
  }
}
</style>
