<template>
  <div style="display: flex; align-items: center; flexDirection: column;">
    <h1 >Checkout</h1>
    <BaseCard style="width: 22rem" justifyContent="center" margin="5rem 0 0 0">
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
              <p style="padding: 0.5rem 0; marginRight: 0.5rem">
                Antal: {{ product.grouped_products.length + 1 }}
              </p>
              <h1 style="font-size: 1rem">
                Totalt:
                {{ (product.grouped_products.length + 1) * product.price }} kr
              </h1>
            </div>
          </div>
        </div>
      </BaseCard>
      <BaseForm :placeOrder="placeOrder"></BaseForm>
    </BaseCard>
  </div>
</template>

<script>
import BaseCard from "@/components/BaseCard";
import BaseForm from "@/components/BaseForm";
export default {
  name: "Checkout",
  props: ["cartList"],
  components: {
    BaseCard,
    BaseForm,
  },
  methods: {
    placeOrder() {
      console.log("order placed");
    },
  },
};
</script>

<style></style>
