<template>
  <div class="container mt-5">
    <!-- Main heading for the Customer Login page -->
    <h1>Customer Login</h1>

    <!-- Login form for the customer -->
    <form @submit.prevent="login" class="dark-form">
      <!-- Input field for the customer's name -->
      <div class="mb-3">
        <label for="customer" class="form-label">Customer Name</label>
        <input
          type="text"
          class="form-control"
          id="customer"
          v-model="customerName"
          required
        />
      </div>
      <!-- Submit button to log in -->
      <button type="submit" class="btn btn-outline-primary">Login</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // Model for storing the customer's name
      customerName: '',
    };
  },
  methods: {
    // Method to handle the login process
    login() {
      // Check if the customer name is provided
      if (this.customerName) {
        // Store the customer data in local storage
        localStorage.setItem(
          'currentCustomer',
          JSON.stringify({ name: this.customerName })
        );
        // Redirect to the products page after successful login
        this.$router.push('/products');
      }
    },
  },
};
</script>

<style scoped>
h1 {
  text-align: center;
}

/* Styling for the form */
.dark-form {
  background-color: #333; 
  padding: 15px; 
  border-radius: 5px;
  color: white; 
  max-width: 400px; 
  margin: 0 auto; 
}
</style>
