<script setup>
import { defineProps, defineEmits, computed } from 'vue';

const props = defineProps(['cart']);
const emit = defineEmits(['remove-item']);

const cartTotal = computed(() =>
  props.cart.reduce((sum, item) => sum + item.price * item.quantity, 0)
);
</script>

<template>
  <div class="shopping-cart">
    <h2>Shopping Cart</h2>
    <ul>
      <li v-for="item in cart" :key="item.id">
        {{ item.name }} - ${{ item.price }} x {{ item.quantity }}
        <button @click="emit('remove-item', item.id)">Remove</button>
      </li>
    </ul>
    <p>Total: ${{ cartTotal }}</p>
  </div>
</template>