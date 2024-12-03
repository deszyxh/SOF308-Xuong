<script setup>
import { ref, onMounted } from 'vue';

// Khai báo các biến cần thiết
const catagory = ref([]);
const catagoriesUrl = 'https://67414054e4647499008d305b.mockapi.io/api/v1/categories';

// Hàm lấy danh sách category từ API
async function getCatagory() {
    try {
        const response = await fetch(catagoriesUrl);
        if (!response.ok) {
            throw new Error('Failed to fetch categories');
        }
        catagory.value = await response.json();
    } catch (error) {
        console.error(error);
        // Bạn có thể hiển thị một thông báo lỗi cho người dùng tại đây
    }
}

// Sử dụng onMounted để gọi getCatagory khi component được mount
onMounted(getCatagory);
</script>

<template>
    <div>
        <h1 class="mb-3 mt-3 text-center">List Catagory</h1>
        <table class="table table-striped">
            <thead class="table-dark">
                <tr>
                    <th>Code</th>
                    <th>Name</th>
                    <th>Description</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="c in catagory" :key="c.id">
                    <td>{{ c.code }}</td>
                    <td>{{ c.name }}</td>
                    <td>{{ c.description }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<style scoped>
/* Thêm một số kiểu CSS nếu cần */
</style>
