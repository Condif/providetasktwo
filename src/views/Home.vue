<template>
  <div class="container">
    <ProductGrid  :products="products" addToCart="addToCart"/>
  </div>
</template>

<script>
// @ is an alias to /src
import ProductGrid from "@/components/ProductGrid"

export default {
  name: 'Home',
  components: {
    ProductGrid
  },
  props: ["products", "addToCart"]
}
</script>
  
<style scoped>
  .container {
    display: flex;
    justify-content: center;
  }
</style>
