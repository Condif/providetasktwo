<template>
  <div id="nav">
    <!-- <div class="logo">

    </div> -->
    <div class="links">
        <router-link to="/" exact>Home</router-link> |
        <router-link to="/about">About</router-link>
    </div>
    <div class="cart" @click="$emit('open')">
      <span class="material-icons">
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
  
}
.links {
    grid-column: 7/13;
    margin-top: 1rem;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

.cart {
    grid-column: 12/13;
    padding: 1rem;
    cursor: pointer;
}
</style>
