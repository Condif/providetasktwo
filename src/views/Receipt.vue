<template>
  <div>
    <BaseCard class="baseCard">
      <div class="header">
        <h2>Tack för ditt köp!</h2>
      </div>
      <div class="productContainer">
        <li
          class="productInfoItem"
          v-for="(product, index) in cartList"
          :key="index"
        >
          <div class="leftContainer">
            <img style="width: 14%" :src="product.images[0].src" />
            <h3 class="margin">{{ product.name }}</h3>
          </div>
          <div class="rightContainer">
            <h4 class="margin">Pris: {{ product.price }}kr</h4>
            <h3 class="margin">x{{ product.grouped_products.length + 1 }}</h3>
            <h3 class="margin">{{ (product.grouped_products.length + 1)*product.price }}kr</h3>
          </div>
        </li>
      </div>

      <div class="personalInfo">
        <div class="fullName">
          <h4 class="margin">Namn: {{ receipt.billing.first_name }}</h4><h4 class="margin">{{ receipt.billing.last_name}}</h4>
        </div>
        <div class="email">
          <h4 class="margin">Email: {{ receipt.billing.email }}</h4>
        </div>
        <div class="email">
          <h3 class="margin">Totalt: {{ totalCost }} kr</h3>
        </div>
        <div class="orderNum">
          <h3 class="margin">Order: {{receipt.order_key}}</h3>
        </div>
      </div>
    </BaseCard>
  </div>
</template>

<script>
import BaseCard from "@/components/BaseCard";
export default {
  props: ["receipt", "cartList"],
  components: {
    BaseCard,
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
};
</script>

<style scoped>
.baseCard {
  width: 50rem;
}

.header {
  display: flex;
  justify-content: center;
  margin: 1rem 0;
}
.productContainer {
  display: flex;
  flex-direction: column;
}

.productInfoItem {
  display: flex;
  justify-content: space-around;
  align-items: center;
}
.leftContainer,
.rightContainer {
  display: flex;
  align-items: center;
  flex-direction: row;
}
.margin {
  margin: 1rem;
}
.fullName {
    display: flex;
}
.orderNum {
    text-align: center;
    margin-top: 3rem;
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
