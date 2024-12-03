<script setup>
const cart = JSON.parse(localStorage.getItem('cart')) || {};
const cartItems = Object.entries(cart);
</script>

<template>
  <div>
    <h1>Sản phẩm trong giỏ hàng</h1>
    <ul>
      <li v-for="[id, item] in cartItems" :key="id">
        <div>
          <!-- Hiển thị ảnh sản phẩm -->
          <img
            :src="item.image || 'https://i5.walmartimages.com/seo/Apple-iPhone-X-64GB-Unlocked-GSM-Phone-w-Dual-12MP-Camera-Space-Gray-B-Grade-Used_15c2b968-bb85-41a4-9292-b017f78fe797.a66ebbf32b6d53b6d6eb14c47434ac04.jpeg'"
            alt="Product Image"
            width="50"
            height="50"
          />
        </div>
        <div>
          Sản phẩm: {{ item.name }} - Số lượng: {{ item.quantity }}
        </div>
      </li>
    </ul>
  </div>
</template>
