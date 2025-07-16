<script setup>
import { ref } from 'vue'
import HelloWorld from './components/HelloWorld.vue'

const msg = ref('Vite + Vue')

window.onload = function () {
  liff.init({
    liffId: "2007757926-Q9RyWWrk"
  }).then(() => {
    if (!liff.isLoggedIn()) {
      liff.login();
    }

    liff.getProfile().then(profile => {
      msg.value = `Hello ${profile.displayName}`;
    }).catch(err => {
      console.error("Lỗi khi lấy profile:", err);
    });

    const idToken = liff.getIDToken();
    console.log("ID Token:", idToken);

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
  <HelloWorld msg="msg" />
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
