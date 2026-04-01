<template>
  <div class="profile">
    <h1>자기소개 페이지</h1>
    <p><strong>이름:</strong> 양보윤</p>
    <p><strong>취미:</strong> 영화 보기, 코딩 공부</p>
    <p><strong>MBTI:</strong> INTP</p>

    <hr />

    <button @click="Home">Home</button>

    <br /><br />

    <RouterLink to="/">Home</RouterLink>

    <br /><br />

    <RouterLink :to="{ name: 'home' }"
      >RouterLink :to="{ name: 'home' }" 로 Home 이동
    </RouterLink>
  </div>
</template>

<script setup>
import { useRouter } from 'vue-router';

const router = useRouter();

const Home = () => {
  router.push('/');
};
</script>

<style scoped>
.profile-page {
  padding: 20px;
}

button {
  padding: 8px 14px;
  cursor: pointer;
}
</style>
