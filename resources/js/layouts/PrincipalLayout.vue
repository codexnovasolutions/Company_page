<script setup>
import Navbar from '@/components/ComponentsCliente/Navbar.vue';
import Footer from '@/components/ComponentsCliente/Footer.vue';
</script>

<template>
  <div>
    <!-- Navbar -->
    <Navbar />

    <!-- Main Content -->
    <main class="flex-grow">
      <slot />
    </main>

    <!-- Footer -->
    <Footer />
  </div>
</template>
