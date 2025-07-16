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
      userData = {
        ...userData,
        userId: profile.userId,
        userName: profile.displayName,

      }
      document.title = 'app title'
      userData.value =  liff.getIDToken()
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
    {{ JSON.stringify(userData) }}
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
