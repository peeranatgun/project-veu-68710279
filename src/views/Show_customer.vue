<template lang="">
  <div class="container my-5">
    <table class="table table-striped-columns">
      <thead>
        <tr class="table table-dark table-striped">
          <th>รหัสลูกค้า</th>
          <th>ชื่อ</th>
          <th>นามสกุล</th>
          <th>เบอร์โทรศัพท์</th>
          <th>username</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="item in customers" :key="item.customer_id">
          <td>{{ item.customer_id }}</td>
          <td>{{ item.firstName }}</td>
          <td>{{ item.lastName }}</td>
          <td>{{ item.phone }}</td>
          <td>{{ item.username }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script setup>
import { ref, onMounted } from "vue";

const customers = ref([]);
const loading = ref(true);
const error = ref(null);

onMounted(async () => {
  try {
    const res = await fetch("http://localhost/project-veu-68710279/php_api/show_customer.php");
    customers.value = await res.json();
    //products.value = data.products;
  } catch (err) {
    error.value = "โหลดข้อมูลไม่สำเร็จ";
  } finally {
    loading.value = false;
  }
});
</script>
