<template>
  <div class="app">
    <Navbar @open="isModalActive = true" />
    <BaseModal v-show="isModalActive" @close="isModalActive = false">
      <Cart :addToCart="addToCart" :removeFromCart="removeFromCart" :cartList="cartList" :productAmount="productAmount"/>
    </BaseModal>
    <main>
      <router-view
        :products="products"
        :cartList="cartList"
        :addToCart="addToCart"
      />
    </main>
  </div>
</template>

<script>
import Navbar from "@/components/TheNavbar";
import Cart from "@/components/Cart";
import BaseModal from "@/components/BaseModal";
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
      cartList: [],
      isModalActive: false,
      productAmount: null,
    };
  },
  components: {
    Navbar,
    Cart,
    BaseModal,
  },
  methods: {
    addToCart(product) {
      const newCartList = [...this.cartList];
      
      if(this.cartList.includes(product)) {
        const index = newCartList.indexOf(product)
        console.log(index);
        const groupedProducts = [...newCartList[index]?.grouped_products]
        console.log(groupedProducts);
        groupedProducts.push(product)
        newCartList[index].grouped_products = groupedProducts;
        this.cartList === newCartList
        console.log("added to amount");
        return
      }
      //add to cartList
      newCartList.push(product);
      this.cartList = newCartList;

      //post to wordpress
    },
    removeFromCart(product) {
      //remove from cartList
      const newCartList = [...this.cartList];
      const index = newCartList.indexOf(product)
      const groupedProducts = [...newCartList[index].grouped_products]

      if(product.grouped_products.length === 0) {
        newCartList.splice(index, 1);
        this.cartList = newCartList;
        return
      }
      
      groupedProducts.splice(index, 1);
      newCartList[index].grouped_products = groupedProducts

      this.cartList = newCartList;
      console.log(this.cartList);
    }
  },
  async created() {
    axios
      .get(url + productEndpoint + keys)
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
