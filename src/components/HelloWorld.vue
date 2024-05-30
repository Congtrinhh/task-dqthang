<script setup>
import { ref, onMounted } from 'vue';

defineProps({
  msg: String,
});

const count = ref(0);

onMounted(async () => {
  //build dữ liệu
  // gọi api từng cục dữ liệu + ghi kết quả ra file
  //fetch()
});

async function sendRequest() {
  //
  const headers = new Headers();
  headers.append(
    'Token',
    'eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6Im1pc2EiLCJpc3MiOiI2NjFiZjkwN2JmZmJiNjNmYWYwYzFiNWEiLCJleHAiOjE3MTcxMTc0Mzh9.VN_lqUk9j2r4oYOna41H1c2L2GJJJu0-4q9YU8Lgqdo'
  );
  headers.append('Username', 'misa');
  //headers.append('Content-Type', 'application/json');
  headers.append(
    'Cookie',
    'AUTH_BEARER_default=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJpYXQiOjE3MTcwMzI5NzgsImp0aSI6ImMzdnkvQXhiaTlTckFOekVaK216NVNROHdENFdEZkxEYU5tQjJuKzdFbmM9IiwiaXNzIjoiZHRpLmhjbS5lZHUudm4iLCJuYmYiOjE3MTcwMzI5NzgsImV4cCI6MTcxNzAzNjU3OCwiZGF0YSI6ImNzcmZUb2tlbnxzOjY0OlwiZWVmMDBmZTEwMjQxNGZlOGY1OTFmOWI3Njc0YmY0NjgzNjIwMzRlMjA2MDExYzQxNDFhMzUwY2VlOGMyMWY0YVwiO2d1ZXN0SWR8czozMjpcIjA1MmE0NTVkMTZmZGUyYjcwMTFhYmQyZmZhZTk4NTdiXCI7In0.oa3zIrw7BvsTy3QsFZOI_hrUe1tNW0cd0J1CWaafCpWbZ2idzYD68tVet4pnU92MIRZVT40K89G9OlvJ_CK1Cw; be=8'
  );
  const myRequest = new Request(
    'https://dti.hcm.edu.vn/sync-data/lms/sendEquipmentInfo',
    {
      method: 'POST',
      headers: headers,
      //mode: 'no-cors',
      //cache: 'default',
      body: JSON.stringify({
        data: {
          hasDeviceInformatics: 2,
        },
        schoolCode: '7900004011',
      }),
    }
  );

  const response = await fetch(myRequest);
  console.log(response);
  if (!response.ok) {
    throw new Error('Network response was not OK');
  }
}
</script>

<template>
  <button @click="sendRequest">Bấm để gửi</button>
  <h1>{{ msg }}</h1>

  <div class="card">
    <button type="button" @click="count++">count is {{ count }}</button>
    <p>
      Edit
      <code>components/HelloWorld.vue</code> to test HMR
    </p>
  </div>

  <p>
    Check out
    <a href="https://vuejs.org/guide/quick-start.html#local" target="_blank"
      >create-vue</a
    >, the official Vue + Vite starter
  </p>
  <p>
    Learn more about IDE Support for Vue in the
    <a
      href="https://vuejs.org/guide/scaling-up/tooling.html#ide-support"
      target="_blank"
      >Vue Docs Scaling up Guide</a
    >.
  </p>
  <p class="read-the-docs">Click on the Vite and Vue logos to learn more</p>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
