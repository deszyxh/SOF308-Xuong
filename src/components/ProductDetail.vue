<script setup>
import { ref } from 'vue';

const props = defineProps(['id']);
const productId = props.id;
const urlProducts =
  'https://67414054e4647499008d305b.mockapi.io/api/v1/products/' + productId;

const product = ref({});
const productImage = ref(
  'https://i5.walmartimages.com/seo/Apple-iPhone-X-64GB-Unlocked-GSM-Phone-w-Dual-12MP-Camera-Space-Gray-B-Grade-Used_15c2b968-bb85-41a4-9292-b017f78fe797.a66ebbf32b6d53b6d6eb14c47434ac04.jpeg'
);

async function getProduct() {
  const response = await fetch(urlProducts);
  const data = await response.json();
  product.value = data;

  // Cập nhật ảnh nếu API trả về ảnh hợp lệ
  if (data.image) {
    productImage.value = data.image;
  }
}
getProduct();

function formatPrice(price) {
  const numberPrice = Number(price) + 1000000;
  if (isNaN(numberPrice)) return 'N/A';
  return numberPrice.toLocaleString('vi-VN') + ' VND';
}

const name = localStorage.getItem('name');
</script>

<template>
  <div class="container">
    <h2>{{ name }}</h2>
    <table class="table table-bordered">
      <thead>
        <tr>
          <th>Image</th>
          <th>Name</th>
          <th>Quantity</th>
          <th>Price</th>
          <th>Description</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>
            <img :src="productImage" alt="Product Image" width="100" />
          </td>
          <td>{{ product.name }}</td>
          <td>{{ product.quantity }}</td>
          <td>{{ formatPrice(product.price) }}</td>
          <td>{{ product.description }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>


<style scoped>
.container {
  margin: 20px;
}

table {
  width: 100%;
  border-collapse: collapse;
}

th,
td {
  padding: 10px;
  text-align: left;
}

img {
  max-width: 100px;
  max-height: 100px;
}
</style>
