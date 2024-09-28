<script setup lang="ts"></script>

<template>
  <!-- Navbar -->
  <div class="container mt-3">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container-fluid">
        <nuxt-link class="navbar-brand" to="/">Multi-Vendor Website</nuxt-link>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarNav"
          aria-controls="navbarNav"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav">
            <li class="nav-item">
              <nuxt-link class="nav-link" to="/">Home</nuxt-link>
            </li>
          </ul>
        </div>
      </div>
    </nav>
    <NuxtPage />
  </div>
</template>

<style>
nav {
  margin-bottom: 20px;
}

.nav-link {
  color: #000; /* Change link color to black */
}

.nav-link:hover {
  color: #007bff; /* Change link color on hover */
}
</style>
