<template>
  <div class="container mt-5">
    <h1>Vendor Dashboard</h1>
    <h2>Products</h2>
    <nuxt-link class="btn btn-outline-success mb-3" to="/vendor/add-product">Add Product</nuxt-link>
    <table class="table table-striped table-dark text-center align-middle">
      <thead>
        <tr>
          <th>ID</th>
          <th>Name</th>
          <th>Price</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <!-- Loop through products and display only those that belong to the logged-in vendor -->
        <tr v-for="product in filteredProducts" :key="product.id">
          <td>{{ product.id }}</td>
          <td>{{ product.name }}</td>
          <td>{{ product.price }}</td>
          <td>
            <button class="btn btn-outline-danger" @click="deleteProduct(product.id)">Delete</button>
          </td>
        </tr>
        <!-- If no products are available -->
        <tr v-if="filteredProducts.length === 0">
          <td colspan="4" class="text-center">No products available for this vendor.</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      products: [], // All products from local storage
      currentVendor: null, // Current vendor from local storage
    };
  },
  computed: {
    // Filter products to show only those belonging to the logged-in vendor
    filteredProducts() {
      return this.products.filter(product => product.vendorId === this.currentVendor.id);
    }
  },
  mounted() {
    // Load products and current vendor from local storage
    const storedProducts = JSON.parse(localStorage.getItem("products")) || [];
    this.products = storedProducts;

    this.currentVendor = JSON.parse(localStorage.getItem('currentVendor'));
    if (!this.currentVendor) {
      this.$router.push('/vendor-login'); // Redirect if no vendor is logged in
    }
  },
  methods: {
    deleteProduct(id) {
      // Confirm deletion prompt
      if (confirm("Are you sure you want to delete this product?")) {
        // Remove the product and update the product list
        this.products = this.products.filter(product => product.id !== id);
        // Update local storage
        localStorage.setItem("products", JSON.stringify(this.products));
      }
    }
  }
};
</script>

<style scoped>
h1, h2 {
  text-align: center;
}
.table {
  margin: 0 auto;
}
th, td {
  vertical-align: middle;
  text-align: center;
}
</style>
