<script setup>
import { ref } from 'vue'
import HelloWorld from './components/MainLayout.vue'

const userData = ref({
  accessToken: '',
  userId: '',
  userName:''
})

window.onload = function () {
  liff.init({
    liffId: "2007757926-Q9RyWWrk"
  }).then(() => {
    if (!liff.isLoggedIn()) {
      liff.login();
    }

    liff.getProfile().then(profile => {
      console.log(profile)
      userData = {
        ...userData,
        userId: profile.userId,
        userName: profile.userName,

      }
      document.title = 'app title'
      userData.value =  liff.getIDToken()
      console.log(userData.value)
    }).catch(err => {
      console.error("Lỗi khi lấy profile:", err);
    });
  }).catch(err => {
    console.error('LIFF init error', err);
    alert('LIFF init failed: ' + JSON.stringify(err));
  });
};
</script>


<template>
  <div>
    <a href="https://vite.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <main-layout :userData="userData" />
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
