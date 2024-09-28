<template>
  <div class="container mt-5">
    <!-- Main heading for the Cart page -->
    <h1>Your Cart</h1>

    <!-- Table displaying the products in the cart -->
    <table class="table table-striped table-dark">
      <thead>
        <tr>
          <!-- Table headers for the product details -->
          <th>ID</th>
          <th>Name</th>
          <th>Price</th>
          <th>Vendor</th>
          <th>Action</th>
        </tr>
      </thead>
      <tbody>
        <!-- Loop through each product in the cart and display its details -->
        <tr v-for="(product, index) in cart" :key="index">
          <td>{{ product.id }}</td>
          <td>{{ product.name }}</td>
          <td>{{ product.price }}</td>
          <td>{{ product.vendor }}</td>
          <td>
            <!-- Button to remove the product from the cart -->
            <button
              class="btn btn-outline-danger"
              @click="removeFromCart(index)"
            >
              Remove
            </button>
          </td>
        </tr>
        <!-- Display this row if the cart is empty -->
        <tr v-if="cart.length === 0">
          <td colspan="5" class="text-center">Your cart is empty</td>
        </tr>
      </tbody>
    </table>

    <!-- Link to navigate back to the products page for more shopping -->
    <nuxt-link class="btn btn-outline-primary" to="/products"
      >Continue Shopping</nuxt-link
    >
  </div>
</template>

<script>
export default {
  data() {
    return {
      // Array to store products added to the cart
      cart: [],
    };
  },
  mounted() {
    // Load the cart data from local storage when the component is mounted
    this.cart = JSON.parse(localStorage.getItem('cart')) || [];
  },
  methods: {
    // Method to remove a product from the cart
    removeFromCart(index) {
      // Remove the product at the specified index
      this.cart.splice(index, 1);
      // Update the cart in local storage
      localStorage.setItem('cart', JSON.stringify(this.cart));
    },
  },
};
</script>

<style scoped>
/* Center the main heading */
h1 {
  text-align: center;
}
</style>
