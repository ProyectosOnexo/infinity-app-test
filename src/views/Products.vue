<template>
  <main class="container">
    <div class="header">
      <h1 class="main-title">Sneaker Dealer</h1>
      <h3 class="main-subtitle">Solo los mas exclusivos.</h3>
    </div>
    <div class="gallery">
      <article
        class="card"
        v-for="product in productos"
        :key="product.product_id"
        @click="goToDetailProduct(product.product_id)"
      >
        <img class="card-img" :src="product.product_image_url" alt="" />
        <div class="info">
          <span class="product-title">{{ product.product_name }}</span>
          <span class="product-price">${{ product.product_price }}</span>
        </div>
      </article>
    </div>
  </main>
</template>

<script>
import router from "@/router";
// @ is an alias to /src
import products from "./../assets/data/products.json";

export default {
  name: "ProductsView",
  data() {
    return {
      productos: products,
    };
  },
  methods: {
    goToDetailProduct(id) {
      router.push({ name: "product", query: { id } });
    },
  },
};
</script>

<style scoped>
.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: 1em;
}

body {
  margin: 0;
  font-family: "Helvetica", sans-serif;
  font-family: "Helvetica Light", sans-serif;
}

.header {
  text-align: center;
}

.main-title {
  background-color: rgb(0, 0, 0);
  color: white;
  margin: 0;
  padding: 0.5em 0;
}

.main-subtitle {
  margin: 0.1em 0;
  font-weight: lighter;
  font-style: italic;
}

.gallery {
  padding-right: 4em;
}
.card {
  overflow: hidden;
  padding: 1em;
  background: #fff;
  border-radius: 0.3rem;
  color: #333;
  width: 10em;
}

.card-img {
  height: 200px;
  width: 100%;
}

.info {
  display: flex;
  flex-direction: column;
  text-align: center;
}
</style>
