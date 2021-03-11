<template>
  <div id="nav">
    <div class="links" style="color: white;">
        <router-link  to="/" exact>Hem</router-link> |
        <router-link  to="/about">Om</router-link> |
        <router-link  to="/mypages">Mina sidor</router-link>
    </div>
    <div v-if="this.$route.name !== 'Checkout' && this.$route.name !== 'Receipt' && this.$route.name !== 'Login'" class="cart end" @click="$emit('open')" >
      <span class="material-icons" style="color:green;">
        shopping_cart
      </span>
    </div>
    <div class="login end"  v-if="!loginInfo.id">
      <router-link to="login">Logga in</router-link>
    </div>
    <div class="login end" v-if="this.$route.name !== 'Login' && loginInfo.id">
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
    grid-column: 8/12;
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
  grid-column: 12/14;
}
.cart {
  grid-column: 11/14;
}

@media screen and (max-width: 570px) {
  .cart {
    grid-column: 2/14;
  }
  .login {
    grid-column: 13/14;
  }
  .links {
    grid-column: 6/14;
  }
}
</style>
