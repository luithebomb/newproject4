<script setup>
import { defineProps, defineEmits } from 'vue';

const props = defineProps(['product']);
const emit = defineEmits(['add-to-cart']);

const addToCart = () => {
  emit('add-to-cart', props.product);
};
</script>

<template>
  <div class="product-item">
    <h2>{{ product.name }}</h2>
    <p>Price: ${{ product.price }}</p>
    <button @click="addToCart">Add to Cart</button>
  </div>
</template>