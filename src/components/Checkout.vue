<script setup>
import { defineProps, defineEmits, computed } from 'vue';

const props = defineProps(['cart']);
const emit = defineEmits(['place-order']);

const cartTotal = computed(() =>
  props.cart.reduce((sum, item) => sum + item.price * item.quantity, 0)
);
</script>

<template>
  <div class="checkout">
    <h2>Checkout</h2>
    <p>Total Price: ${{ cartTotal }}</p>
    <button @click="emit('place-order')">Place Order</button>
  </div>
</template>