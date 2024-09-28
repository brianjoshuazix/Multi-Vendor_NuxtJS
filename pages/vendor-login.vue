<template>
  <div class="container mt-5">
    <!-- Heading for the vendor login page -->
    <h1>Vendor Login</h1>

    <!-- Login form for vendors, with a dark theme applied via the class "dark-form" -->
    <form @submit.prevent="login" class="dark-form">
      <!-- Dropdown to select a vendor -->
      <div class="mb-3">
        <label for="vendor" class="form-label">Select Vendor</label>
        <!-- Select input bound to the selectedVendor data property -->
        <select class="form-control" v-model="selectedVendor" required>
          <!-- Loop through the vendors array and create an option for each vendor -->
          <option v-for="vendor in vendors" :key="vendor.id" :value="vendor">
            {{ vendor.name }}
          </option>
        </select>
      </div>

      <!-- Login button to submit the form -->
      <button type="submit" class="btn btn-outline-primary">Login</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // List of vendors available for login
      vendors: [
        { id: 1, name: "Vendor A" }, 
        { id: 2, name: "Vendor B" }, 
        { id: 3, name: "Vendor C" }, 
      ],
      selectedVendor: null, // Holds the vendor selected from the dropdown
    };
  },
  methods: {
    // Login method that triggers when the form is submitted
    login() {
      // Check if a vendor is selected
      if (this.selectedVendor) {
        // Save the selected vendor details in local storage
        localStorage.setItem(
          "currentVendor",
          JSON.stringify(this.selectedVendor)
        );
        // Redirect the user to the vendor dashboard after successful login
        this.$router.push("/vendor/dashboard");
      }
    },
  },
};
</script>

<style scoped>
h1 {
  text-align: center;
}
.dark-form {
  background-color: #333; 
  padding: 15px; 
  border-radius: 5px;
  color: white; 
  max-width: 400px;
  margin: 0 auto;
}
</style>
