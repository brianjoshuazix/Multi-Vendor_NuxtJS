<template>
  <div class="container mt-5">
    <!-- Link to the cart page displaying the number of items in the cart -->
    <nuxt-link class="btn btn-outline-primary float-right mb-3" to="/cart">
      Cart ({{ cart.length }})
    </nuxt-link>

    <!-- Main heading for the Vendors section -->
    <h1>Vendors</h1>

    <!-- Vendor Cards Section -->
    <div class="row">
      <!-- Vendor Card A -->
      <div class="col-md-4 text-center">
        <!-- Clicking when selecting Vendor A -->
        <div class="vendor-card" @click="selectVendor(vendorA)">
          <img src="public/images/1.jpg" alt="Vendor A" class="img-fluid" />
          <h3>Vendor A</h3>
        </div>
      </div>

      <!-- Vendor Card B -->
      <div class="col-md-4 text-center">
        <!-- Clicking when selecting Vendor B -->
        <div class="vendor-card" @click="selectVendor(vendorB)">
          <img src="/public/images/3.jfif" alt="Vendor B" class="img-fluid" />
          <h3>Vendor B</h3>
        </div>
      </div>

      <!-- Vendor Card C -->
      <div class="col-md-4 text-center">
        <!-- Clicking when selecting Vendor C -->
        <div class="vendor-card" @click="selectVendor(vendorC)">
          <img src="public/images/2.jfif" alt="Vendor C" class="img-fluid" />
          <h3>Vendor C</h3>
        </div>
      </div>
    </div>

    <!-- Selected Vendor's Products Section -->
    <div v-if="selectedVendor" class="mt-5" text-align="center">
      <!-- Heading displaying the name of the selected vendor -->
      <h2>{{ selectedVendor.name }}'s Products</h2>

      <!-- Table displaying products for the selected vendor -->
      <table class="table table-striped table-dark">
        <thead>
          <tr>
            <th>ID</th>
            <th>Name</th>
            <th>Price</th>
            <th>Add to Cart</th>
          </tr>
        </thead>
        <tbody>
          <!-- Loop through the products of the selected vendor -->
          <tr v-for="product in getVendorProducts(selectedVendor.id)" :key="product.id">
            <td>{{ product.id }}</td>
            <td>{{ product.name }}</td>
            <td>{{ product.price }}</td>
            <td>
              <!-- Button to add the product to the cart -->
              <button class="btn btn-outline-success" @click="addToCart(product)">Add to Cart</button>
            </td>
          </tr>

          <!-- Display message if there are no products for the selected vendor -->
          <tr v-if="getVendorProducts(selectedVendor.id).length === 0">
            <td colspan="4" class="text-center">No products available</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // List of all products, loaded from local storage
      products: JSON.parse(localStorage.getItem("products")) || [],
      // Array to store cart items
      cart: [],
      // Currently selected vendor, initially null
      selectedVendor: null,
      // Vendor A object with ID and name
      vendorA: { id: 1, name: 'Vendor A' },
      // Vendor B object with ID and name
      vendorB: { id: 2, name: 'Vendor B' },
      // Vendor C object with ID and name
      vendorC: { id: 3, name: 'Vendor C' },
    };
  },
  mounted() {
    // Load products and cart items from local storage when component is mounted
    this.products = JSON.parse(localStorage.getItem('products')) || [];
    this.cart = JSON.parse(localStorage.getItem('cart')) || [];
  },
  methods: {
    // Method to set the selected vendor when a vendor card is clicked
    selectVendor(vendor) {
      this.selectedVendor = vendor;
    },
    // Method to get products of the selected vendor based on vendor ID
    getVendorProducts(vendorId) {
      return this.products.filter(product => product.vendorId === vendorId);
    },
    // Method to add a product to the cart and save the updated cart to local storage
    addToCart(product) {
      this.cart.push(product);
      localStorage.setItem('cart', JSON.stringify(this.cart));
      alert(`${product.name} has been added to your cart!`); // Alert to confirm the addition of the product
    }
  },
};
</script>

<style scoped>
/* Center the main heading */
h1 {
  text-align: center;
}

/* Styles for the vendor card */
.vendor-card {
  cursor: pointer; /* Changes cursor to pointer on hover */
  border: 1px solid #ccc; /* Light border around the card */
  border-radius: 8px; /* Rounded corners */
  padding: 20px; /* Padding inside the card */
  margin: 20px 0; /* Margin between cards */
  transition: box-shadow 0.3s ease; /* Smooth transition effect for shadow */
}

/* Hover effect for vendor card */
.vendor-card:hover {
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2); /* Box shadow on hover */
}

/* Styles for images inside the vendor cards */
img {
  max-width: 100%; /* Ensures the image fits the card */
  height: auto; /* Maintains aspect ratio */
}
</style>
