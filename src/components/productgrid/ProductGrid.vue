<template>
  <div class="container">
    <div class="content">
      <div class="card" v-for="product in products" :key="product.id">
        <div class="cardContent">
          <h1>{{ product.name }}</h1>
          <p>
            Lorem ipsum dolor sit amet consectetur, adipisicing elit. Quos ad
            pariatur deserunt! Quidem ea voluptatibus fugit laudantium
            cupiditate! Nisi, officiis! Magni ab officiis temporibus ipsum
            repellendus doloremque laudantium distinctio animi.
          </p>
          <img :src="product.images[0].src" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProductGrid",
  props: ["products"],
};
</script>

<style scoped>
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

.card {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
}

.cardContent {
  display: flex;
  flex: 1 1 150px;
  margin: 5px;
  flex-direction: column;
  justify-content: space-between;
  padding: 1rem;
  box-shadow: 2px 2px 4px 1px black;
  background: rgb(247, 247, 245);
  border-radius: 1rem;
}

h1 {
  font-size: clamp(0.2rem, 1rem, 1.5rem);
}

@media screen and (max-width: 600px) {
  .content {
    grid-template: 1fr / 1fr;
  }
}
@media screen and (max-width: 1250px) and (min-width: 600px) {
  .content {
    grid-template: 1fr 1fr / 1fr 1fr;
  }
}
</style>
