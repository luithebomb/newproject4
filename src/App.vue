<script setup>
import { ref } from 'vue';
import ProductItem from './components/ProductItem.vue';
import ShoppingCart from './components/ShoppingCart.vue';
import Checkout from './components/Checkout.vue';

const products = ref([]);

const cart = ref([]);
const newProduct = ref({ name: '', price: '' });

const addNewProduct = () => {
  if (newProduct.value.name && newProduct.value.price) {
    products.value.push({
      id: products.value.length + 1,
      name: newProduct.value.name,
      price: Number(newProduct.value.price)
    });
    newProduct.value = { name: '', price: '' };
  }
};

const addToCart = (product) => {
  const item = cart.value.find((p) => p.id === product.id);
  if (item) {
    item.quantity++;
  } else {
    cart.value.push({ ...product, quantity: 1 });
  }
};

const removeFromCart = (productId) => {
  cart.value = cart.value.filter((p) => p.id !== productId);
};

const placeOrder = () => {
  alert('Order placed successfully!');
  cart.value = [];
};
</script>

<template>
  <div class="container">
    <h1>Online Shopping Cart</h1>

    <div class="product-form">
      <input v-model="newProduct.name" placeholder="Product Name" />
      <input v-model="newProduct.price" type="number" placeholder="Price" />
      <button @click="addNewProduct">Add Product</button>
    </div>

    <div class="product-list">
      <ProductItem v-for="product in products" :key="product.id" :product="product" @add-to-cart="addToCart" />
    </div>

    <ShoppingCart :cart="cart" @remove-item="removeFromCart" />
    <Checkout :cart="cart" @place-order="placeOrder" />
  </div>
</template>
