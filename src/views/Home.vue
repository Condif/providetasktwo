<template>
  <div class="container">
    <ProductGrid  :products="products"/>
  </div>
</template>

<script>
// @ is an alias to /src
import ProductGrid from "@/components/productgrid/ProductGrid"

export default {
  name: 'Home',
  components: {
    ProductGrid
  },
  props: ["products"]
}
</script>
  
<style scoped>
  .container {
    display: flex;
    justify-content: center;
  }
</style>
