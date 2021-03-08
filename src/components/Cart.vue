<template>
    <div class="cart">
        <BaseCard
          flexDirection="row"
          boxShadow="none"
          v-for="(product, index) in cartList"
          :key="index"
        >
          <img style="width: 50%" :src="product.images[0].src" />
          <div
            style="display: flex;  flexDirection: column; width:50%; padding: 0.2rem"
          >
            <div style="display: flex; align-items: center; padding: 0.1rem;">
              <h1 style="font-size: 1rem">{{ product.name }}</h1>
            </div>
            <div
              style="display: flex; flexDirection: column; align-items: flex-start; padding: 0.5rem 0 "
            >
               <p style="padding: 0.5rem 0">Pris: {{ product.price }} :-</p>
              <div style="display: flex; align-items: center; justifyContent: space-between">
                <p style="padding: 0.5rem 0">Antal: {{product.grouped_products.length + 1}}</p>
                <button style="margin: 0 0.5rem;" @click="addToCart(product)">
                  +
                </button>
                <button @click="removeFromCart(product)">-</button>
              </div>
              
            </div>
            <h1 style="font-size: 1rem">Totalt:</h1>
          </div>
        </BaseCard>
    </div>
</template>

<script>
import BaseCard from "@/components/BaseCard";
export default {
    name: "Cart",
    props: ["addToCart", "removeFromCart", "cartList", "productAmount"],
    components: {
        BaseCard,
    },
    
}
</script>

<style scoped>
</style>