<template>
  <div class="card">
    <img
      class="card-img-top"
      src="https://i5.walmartimages.com/seo/Apple-iPhone-X-64GB-Unlocked-GSM-Phone-w-Dual-12MP-Camera-Space-Gray-B-Grade-Used_15c2b968-bb85-41a4-9292-b017f78fe797.a66ebbf32b6d53b6d6eb14c47434ac04.jpeg"
      alt="Product Image"
    />
    <div class="card-body">
      <h5 class="card-title">{{ productName }}</h5>
      <p class="card-text">Mã sản phẩm: {{ productId }}</p>
      <div class="d-flex justify-content-between">
        <a :href="urlDetail" class="btn btn-primary">
          <BIconEye /> Xem chi tiết
        </a>
        <button
          class="btn btn-success"
          @click="handleAddToCart(productId, productName)"
        >
          <BIconCart /> Thêm vào giỏ
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { BIconCart, BIconEye } from 'bootstrap-icons-vue';

// Nhận props từ cha
const props = defineProps({
  id: String,
  productName: String,
});

// Khai báo các biến cần thiết
const productId = props.id;
const productName = props.productName;
const urlDetail = `/product/${productId}`;

// Hàm xử lý thêm sản phẩm vào giỏ hàng
function handleAddToCart(id, name) {
  let cart = JSON.parse(localStorage.getItem('cart')) || {};
  if (cart[id]) {
    cart[id].quantity++;
  } else {
    cart[id] = { name, quantity: 1 };
  }
  localStorage.setItem('cart', JSON.stringify(cart));
  alert(`Sản phẩm "${name}" đã được thêm vào giỏ hàng!`);
}
</script>

<style scoped>
.card {
  width: 18rem;
  margin: 1rem auto;
  border: 1px solid #ddd;
  box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
}
.card-img-top {
  object-fit: cover;
  height: 200px;
}
.card-body {
  padding: 1rem;
}
.card-title {
  font-size: 1.25rem;
  font-weight: bold;
}
.card-text {
  font-size: 1rem;
  margin-bottom: 1rem;
}
.d-flex {
  display: flex;
  justify-content: space-between;
}
.btn {
  display: flex;
  align-items: center;
}
</style>
