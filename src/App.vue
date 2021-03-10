<template>
  <div class="app">
    <Navbar @open="isModalActive = true" />
    <BaseModal v-show="isModalActive" @close="isModalActive = false">
      <Cart :closeModal="closeModal"  @close="isModalActive = false" :addToCart="addToCart" :removeFromCart="removeFromCart" :cartList="cartList" :productAmount="productAmount"/>
    </BaseModal>
    <main>
      <router-view
        :products="products"
        :cartList="cartList"
        :addToCart="addToCart"
        @newOrder="createReceipt"
        :receipt="receipt"
        
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
      receipt: {},
    };
  },
  components: {
    Navbar,
    Cart,
    BaseModal,
  },
  methods: {
    createReceipt(value) {
      this.receipt = value
    },
    closeModal () {
      this.isModalActive = false
    },
    addToCart(product) {
      const newCartList = [...this.cartList];
      
      if(this.cartList.includes(product)) {
        const index = newCartList.indexOf(product)
        const groupedProducts = [...newCartList[index]?.grouped_products]
        groupedProducts.push(product)
        newCartList[index].grouped_products = groupedProducts;
        this.cartList === newCartList
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
      
      groupedProducts.shift(1);
      newCartList[index].grouped_products = groupedProducts

      this.cartList = newCartList;
    }
  },
  async created() {
    axios
      .get(url + productEndpoint + keys)
      .then((res) => {
        this.products = res.data;
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
span {
    user-select: none; /* standard syntax */
    -webkit-user-select: none; /* webkit (safari, chrome) browsers */
    -moz-user-select: none; /* mozilla browsers */
    -khtml-user-select: none; /* webkit (konqueror) browsers */
    -ms-user-select: none; /* IE10+ */
}
body {
  background: rgb(243, 243, 243);
}




.app {
  display: grid;
  grid-template: auto 1fr auto / auto 1fr auto;
}

main {
  grid-column: 1 / 3;
  justify-content: center;
  display: flex;
  margin-top: 8rem;
}

li {
  list-style-type: none;
}
</style>
