<template>
  <div class="container mt-5">
    <!-- Main heading for the page -->
    <h1>Add New Product</h1>

    <!-- Center the form horizontally within the container -->
    <div class="d-flex justify-content-center">
      <!-- Form for adding a new product -->
      <form
        @submit.prevent="addProduct"
        class="w-50 p-4 bg-dark text-white rounded"
      >
        <!-- Input for the product name -->
        <div class="mb-3">
          <label for="name" class="form-label">Product Name</label>
          <input
            type="text"
            class="form-control bg-dark text-white border-secondary"
            id="name"
            v-model="newProduct.name"
            required
          />
        </div>

        <!-- Input for the product price -->
        <div class="mb-3">
          <label for="price" class="form-label">Product Price</label>
          <input
            type="number"
            class="form-control bg-dark text-white border-secondary"
            id="price"
            v-model="newProduct.price"
            required
          />
        </div>

        <!-- Submit button to add the product -->
        <button type="submit" class="btn btn-outline-success">
          Add Product
        </button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // Object to hold the new product's details
      newProduct: {
        id: null, // Product ID, will be generated automatically
        name: "", // Product name
        price: "", // Product price
      },
      currentVendor: null, // To store the currently logged-in vendor
    };
  },
  mounted() {
    // When the component is mounted, retrieve the current vendor from local storage
    this.currentVendor = JSON.parse(localStorage.getItem("currentVendor"));

    // If no vendor is found, redirect to the vendor login page
    if (!this.currentVendor) {
      this.$router.push("/vendor-login");
    }
  },
  methods: {
    // Method to handle the product addition
    addProduct() {
      // Retrieve existing products from local storage or initialize with an empty array
      const storedProducts = JSON.parse(localStorage.getItem("products")) || [];

      // Generate a new ID for the product
      this.newProduct.id = storedProducts.length
        ? Math.max(...storedProducts.map((p) => p.id)) + 1
        : 1;

      // Set the vendor ID and name for the new product
      this.newProduct.vendorId = this.currentVendor.id;
      this.newProduct.vendor = this.currentVendor.name;

      // Add the new product to the stored products array
      storedProducts.push(this.newProduct);

      // Save the updated products array back to local storage
      localStorage.setItem("products", JSON.stringify(storedProducts));

      // Redirect back to the vendor dashboard
      this.$router.push("/vendor/dashboard");
    },
  },
};
</script>

<style scoped>
/* Center align the main heading */
h1 {
  text-align: center;
}
</style>
