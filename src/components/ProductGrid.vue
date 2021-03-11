<template>
  <div class="container">
    <div class="content">
      <BaseCard v-for="product in products" :key="product.id">
        <h1>{{ product.name }}</h1>
        <div class="cardTextBox">
         <span v-html="product.short_description"></span>
        </div>
        <img :src="product.images[0].src" />
        <div class="cardFooter">
          <BaseButton  @onClick="addToCart(product)" class="baseButton"
            >Add to cart
          </BaseButton>
        </div>
      </BaseCard>
    </div>
  </div>
</template>

<script>
import BaseButton from "./BaseButton";
import BaseCard from "./BaseCard";
export default {
  name: "ProductGrid",
  props: ["products", "addToCart"],
  components: {
    BaseButton,
    BaseCard,
  },
};
</script>

<style scoped>
span { 
    display:block;
    width:100%;
    word-wrap:break-word;
}
.cardFooter {
  margin-top: 2rem;
}
.container {
  display: flex;
  max-width: 80%;
}

.content {
  display: grid;
  grid-template: repeat(4, 1fr) / repeat(4, 1fr);
  flex-wrap: wrap;
  justify-content: center;
  height: auto;
}

p {
  font-size: clamp(1rem, -0.1250rem + 3.0000vw, 1.1rem);
}

h1 {
  font-size: clamp(2rem, -0.1250rem + 5.0000vw, 2.3rem);
}

.cardTextBox {
  display: flex;
  align-items: center;
  height: 10rem;
  margin: 1rem 0;
}

@media screen and (max-width: 410px) {
  .content {
    grid-template: 1fr / 1fr;
  }
  h1 {
  font-size: 2rem;
}
span {
    font-size: 0.9rem;
  }
}

@media screen and (max-width: 890px) and (min-width: 411px) {
  .content {
    grid-template: 1fr / 1fr;
  }
  h1 {
  font-size: 2.5rem;
}
span {
    font-size: 1.2rem;
  }
}
@media screen and (max-width: 1400px) and (min-width: 890px) {
  .content {
    grid-template: 1fr 1fr / 1fr 1fr;
  }
  h1 {
  font-size: 2.5rem;
  }
  span {
    font-size: 1.2rem;
  }
}
</style>
