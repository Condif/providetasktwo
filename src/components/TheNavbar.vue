<template>
  <div id="nav">
    <div class="links" style="color: white;">
        <router-link  to="/" exact>Home</router-link> |
        <router-link  to="/about">About</router-link>
    </div>
    <div v-if="this.$route.name !== 'Checkout' && this.$route.name !== 'Receipt'" class="cart" @click="$emit('open')" >
      <span class="material-icons" style="color:green;">
        shopping_cart
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: "Navbar",
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
    grid-row: 1/10;
    margin-top: 1rem;
}

#nav a {
  font-weight: bold;
  color: white;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

.cart {
    grid-column: 12/13;
    grid-row: 4/10;
    cursor: pointer;
    
}
</style>
