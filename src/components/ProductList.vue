<script setup>
import { ref } from 'vue';
import ProductItem from './ProductItem.vue';

// Tạo biến lưu trữ danh sách sản phẩm
const products = ref([]);

// Địa chỉ API lấy sản phẩm
const urlProducts = 'https://67414054e4647499008d305b.mockapi.io/api/v1/products';

// Hàm lấy danh sách sản phẩm từ API
async function getProduct() {
  try {
    const response = await fetch(urlProducts);
    products.value = await response.json();
  } catch (error) {
    console.error('Error fetching products:', error);
  }
}

// Gọi hàm getProduct khi component được load
getProduct();

// Hàm định dạng giá sản phẩm
function formatPrice(price) {
  const numberPrice = Number(price) + 1000000; // Thêm 1 triệu vào giá sản phẩm
  if (isNaN(numberPrice)) return 'N/A'; // Nếu không phải số, trả về 'N/A'
  return numberPrice.toLocaleString('vi-VN') + ' VND'; // Định dạng tiền Việt
}

// Lưu tên vào localStorage
localStorage.setItem('name', 'SD19312');
</script>

<template>
  <div class="container">
    <h1 class="mb-3 mt-3 text-center">Danh Sách Sản Phẩm</h1>

    <!-- Liên kết đến trang giỏ hàng -->
    <router-link to="/cart">
      Xem giỏ hàng
    </router-link>

    <div class="row">
      <!-- Lặp qua từng sản phẩm và hiển thị -->
      <div class="col-3 g-3" v-for="product in products" :key="product.id">
        <ProductItem :id="product.id" :productName="product.name">
          <template #productName>
            {{ product.name }}
          </template>
          <template #productPrice>
            {{ formatPrice(product.price) }}
          </template>
        </ProductItem>
      </div>
    </div>
  </div>
</template>
