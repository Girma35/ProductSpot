<script setup lang="ts">
import { computed, ref } from 'vue'
import Blue from '../assets/socks_blue.jpeg'
import Green from '../assets/socks_green.jpeg'
import './ProductDisplay.css' 

const props = defineProps({
  premium: {
    type: Boolean,
    default: false
  },
  cart: {
    type: Object as () => { count: number } | null,
    default: null
  }
})

const productName = ref("Premium Cotton")
const brand = ref("akile")

const title = computed(() => `${productName.value} ${brand.value} socks`)

const selectedVariant = ref(0)

const variants = ref([
  { color: "Green", image: Green, quantity: 0 },
  { color: "Blue", image: Blue, quantity: 50 },
])

const shipping = computed(() => {
    if (props.premium){
        return "free"
    }else {
        return "$2.99 "
    }
})
const isOnSale = computed(() => variants.value[selectedVariant.value].quantity > 0)

const Emit = defineEmits(["addToCart"])

const add_to_cart = () => {
    Emit("addToCart")
}

const image = computed(() => variants.value[selectedVariant.value].image)
const qty = computed(() => variants.value[selectedVariant.value].quantity)

const updateVariant = (index: number) => {
  selectedVariant.value = index
}
const available = computed(() => {
  const cartItems = props.cart?.count || 0
  return Math.max(0, qty.value - cartItems) // Ensures never negative
})

const details = computed(() => [
  { label: "Name", value: "Premium Cotton Socks" },
  { label: "Brand", value: "ComfortWear" },
  { label: "Material", value: "Cotton, Polyester, Elastane" },
  { label: "Sizes", value: "S, M, L, XL" },
  { label: "Colors", value: "Blue, Black, White, Gray" },
  { label: "Price", value: "$9.99" },
  { label: "On Sale", value: isOnSale.value ? "Yes" : "No" },
  { label: "Rating", value: "4.7 / 5" },
  {label:"shipping",value:shipping.value},
  { label: "Stock", value: `${available.value} available` },
  { label: "Description", value: "Experience all-day comfort with our breathable and durable cotton socks — perfect for everyday wear." },
  { label: "Features", value: "Moisture-wicking, Reinforced heel/toe, Machine washable, Eco-friendly packaging" },
])
</script>

<template>
  <div class="product-display">
    <div class="product-card">
      <div class="product-image">
        <img :src="image" alt="Image of product" />
      </div>

      <div class="variants">
        <h3>Available Colors:</h3>
        <div class="variant-container">
          <div
            v-for="(variant, index) in variants"
            :key="variant.color"
            class="variant-pill"
            :class="{ active: index === selectedVariant }"
            @mouseover="updateVariant(index)"
            :style="{ backgroundColor: variant.color }"
          ></div>
        </div>
      </div>

      <div class="product-info">
        <h1 class="product-title">{{ title }}</h1>
        <p class="product-sale" v-if="isOnSale">✨ Now on Sale!</p>
        <p class="product-sale out" v-else>Out of Stock</p>

        <ul class="product-details">
          <li v-for="detail in details" :key="detail.label">
            <strong>{{ detail.label }}:</strong> {{ detail.value }}
          </li>
        </ul>

        <div class="cart">
         
          <button @click="add_to_cart" :disabled="!isOnSale" >Add to cart</button>
        </div>
      </div>
    </div>
  </div>
</template>