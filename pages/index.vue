<template>
  <div class="container mt-5">
    <!-- Main Header for the Webpage -->
    <h1>Welcome to the Multi-Vendor Website</h1>

    <!-- Navigation Links -->
    <div class="text-center mb-4">
      <nuxt-link class="btn btn-outline-primary mx-2" to="/vendor-login">Vendor Login</nuxt-link>
      <nuxt-link class="btn btn-outline-success mx-2" to="/customer-login">Customer Login</nuxt-link>
    </div>

    <!-- Sub-Header  -->
    <h2>Available Products</h2>

    <!-- Products Table -->
    <table class="table table-striped table-dark text-center align-middle">
      <thead>
        <tr>
          <th>ID</th>
          <th>Name</th>
          <th>Price</th>
          <th>Details</th>
        </tr>
      </thead>
      <tbody>
        <!-- Loop through the products array and render each product row -->
        <tr v-for="product in products" :key="product.id">
          <td>{{ product.id }}</td>
          <td>{{ product.name }}</td>
          <td>{{ product.price }}</td>
          <td>
            <nuxt-link
              class="btn btn-outline-warning"
              :to="`/product/${product.id}`"
            >View Details</nuxt-link>
          </td>
        </tr>
        <!-- If there are no products -->
        <tr v-if="products.length === 0">
          <td colspan="4" class="text-center">No products available</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // Initialize an empty array to store product data
      products: [],
    };
  },
  mounted() {
    // Load products from local storage
    const storedProducts = JSON.parse(localStorage.getItem("products"));
    // Set products to the loaded data or an empty array
    this.products = storedProducts || [];
  },
};
</script>

<style scoped>
h1,
h2 {
  text-align: center;
}

.table {
  margin: 0 auto;
}

th,
td {
  vertical-align: middle;
  text-align: center;
}

.btn {
  margin: 0 10px;
}
</style>
