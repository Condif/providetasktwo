<template>
  <div class="app">
    <Navbar />
    <main>
      <router-view :products="products" />
    </main>
    <Cart />
  </div>
</template>

<script>
import Navbar from "@/components/navbar/Navbar";
import Cart from "@/components/cart/Cart";
import axios from "axios";

const url = "https://ftest.dev3.provideit.se";
const productEndpoint = "/wp-json/wc/v3/products?";
const keys =
  "consumer_key=ck_9b6f2b633c777a37bccb7553cf8b1d47c7e3447c&consumer_secret=cs_55cfbde055597f2eb86077159500e65f1423ac7e";

export default {
  name: "App",
  data() {
    return {
      products: [],
    };
  },
  components: {
    Navbar,
    Cart,
  },
  async created() {
    axios
      .get(url + productEndpoint  + keys )
      .then((res) => {
        this.products = res.data;
        console.log(this.products);
      })
      .catch((err) => console.log(err));
  },
};
</script>

<style>
* {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 0;
  box-sizing: border-box;
}

.app {
  display: grid;
  grid-template: auto 1fr auto / auto 1fr auto;
}

main {
  grid-column: 1 / 3;
  justify-content: center;
  display: flex;
}
</style>
