<script setup lang="ts">
import { ref } from 'vue';

const product = ref("socks")
const desc = ref("Experience unmatched comfort with our premium cotton socks — soft, breathable, and designed for all-day wear. Perfect for everyday use or a stylish touch to your outfit.")
</script>
 
<template>
  <div class="product-display">
    <div class="product-container">
       <h1>{{ product }}</h1>
      <div class="product-info">
       
        <p>{{ desc }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.product-display {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background: linear-gradient(145deg, #e0e0e0, #ffffff);
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.product-container {
  background: #f5f5f5;
  border-radius: 20px;
  box-shadow: 10px 10px 25px #d1d1d1, -10px -10px 25px #ffffff;
  padding: 2rem 3rem;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.product-container:hover {
  transform: translateY(-10px);
  box-shadow: 10px 10px 30px rgba(0, 0, 0, 0.1);
}

.product-info h1 {
  font-size: 2rem;
  color: #333;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.1);
}
</style>
