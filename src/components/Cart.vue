<template>
  <div class="cart">
    <BaseCard
      flexDirection="row"
      boxShadow="1px 1px 4px green"
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
          <p style="padding: 0.5rem 0">Pris: {{ product.price }} kr</p>
          <div
            style="display: flex; align-items: center; justifyContent: space-between"
          >
            <p style="padding: 0.5rem 0">
              Antal: {{ product.grouped_products.length + 1 }}
            </p>
            <div typ="button" style="margin: 0.1rem 0.3rem 0 1rem;">
              <span
                style="color: lightgreen; cursor: pointer;"
                class="material-icons"
                @click="addToCart(product)"
              >
                add_circle
              </span>
            </div>
            <div typ="button" style="margin-top: 0.1rem;">
              <span
                style="color: pink; cursor: pointer;"
                class="material-icons"
                @click="removeFromCart(product)"
              >
                remove_circle
              </span>
            </div>
          </div>
        </div>
        <h1 style="font-size: 1rem">
          Totalt: {{ (product.grouped_products.length + 1) * product.price }} kr
        </h1>
      </div>
    </BaseCard>
    <h1 style="font-size: 1rem; text-align: center; padding: 1rem;">Totalt: {{ totalCost }} kr</h1>
    <div style="display: flex; justifyContent: center; padding: 1rem;"><BaseButton  @onClick="goToCheckout()" padding="0.8rem 3rem">Betala</BaseButton></div>
    
  </div>
</template>

<script>
import BaseCard from "@/components/BaseCard";
import BaseButton from "@/components/BaseButton";

export default {
  name: "Cart",
  props: ["addToCart", "removeFromCart", "cartList", "productAmount", "closeModal"],
  components: {
    BaseCard,
    BaseButton,
  },
  computed: {
    totalCost() {
      let totalCost = 0;
      this.cartList.forEach((product) => {
        totalCost =
          totalCost + (product.grouped_products.length + 1) * product.price;
      });
      return totalCost;
    },
  },
  methods: {
    goToCheckout() {
      this.closeModal()
      this.$router.push("/checkout")
      
    } 
  }
};
</script>

<style scoped>
.cart {
  box-shadow: 5px 2px 4px green;
  overflow: auto;
  
}
/* Hide scrollbar for Chrome, Safari and Opera */
::-webkit-scrollbar {
  display: none;
  -ms-overflow-style: none;  /* IE and Edge */
  scrollbar-width: none;  /* Firefox */
}
</style>
