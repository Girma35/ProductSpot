<script setup lang="ts">
import {ref } from "vue"
import productDisplay from "./components/productDisplay.vue"
const premium = ref(false)
let cart = ref(0)
const updateCart = () =>{
  cart.value += 1
}

</script>

<template>
  <productDisplay :premium ="premium" @addToCart="updateCart" :cart="cart"></productDisplay>
  <div>
🛒 Cart: {{ cart }}
  </div> 
</template>

