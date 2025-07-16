<script setup>
import { ref } from 'vue'
import MainLayout from './components/MainLayout.vue'

const userData = ref({
  accessToken: '',
  userId: '',
  userName: ''
})
const isLoggedIn = ref(false) 
window.onload = function () {
  liff.init({
    liffId: "2007757926-Q9RyWWrk"
  }).then(() => {
    if (!liff.isLoggedIn()) {
      liff.login()
      return
    }

    liff.getProfile().then(profile => {
      userData.value.userId = profile.userId
      userData.value.userName = profile.displayName
      userData.value.accessToken = liff.getIDToken()
      document.title = 'app title'
      isLoggedIn.value = true 
    }).catch(err => {
      console.error("Lỗi khi lấy profile:", err)
    })
  }).catch(err => {
    console.error('LIFF init error', err)
    alert('LIFF init failed: ' + JSON.stringify(err))
  })
}
</script>

<template>
  <div v-if="!isLoggedIn">
    <p>Đang đăng nhập, vui lòng chờ...</p>
  </div>
   <div v-else>
    <main-layout :userData="userData" />
  </div>
</template>
