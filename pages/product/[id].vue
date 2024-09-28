<template>
  <div class="container mt-5">

    <!-- If the product exists -->
    <div v-if="product" class="text-center">
      <!-- Display product Name  -->
      <h1><strong>Product Name: </strong>{{ product.name }}</h1>
      <!-- Display Product Price  -->
      <h2><strong>Price: </strong> {{ product.price }}</h2>

      <!-- Redirect to home  -->
      <nuxt-link class="btn btn-outline-primary mt-3" to="/"
        >Back to Home</nuxt-link
      >
    </div>
    <!-- If the product is not found -->
    <div v-else class="text-center">
      <h2>Product not found</h2>
      <nuxt-link class="btn btn-outlin-primary mt-3" to="/"
        >Go Back Home</nuxt-link
      >
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // Initialize an empty array to store product data
      product: null,
    };
  },
  mounted() {
    // Get the ID from the route
    const productId = this.$route.params.id;
    // Load products from local storage
    const storedProducts = JSON.parse(localStorage.getItem("products")) || [];
    // Find the product by ID
    this.product = storedProducts.find((p) => p.id === Number(productId));
    // If product is not found
    if (!this.product) {
      console.warn(`Product with ID ${productId} not found.`);
    }
  },
};
</script>

<style scoped>
h1 {
  color: #333;
  text-align: center;
  margin-top: 10px;
}
h2 {
  text-align: center;
  margin-top: 10px;
}
</style>
