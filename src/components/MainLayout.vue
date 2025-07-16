<script setup>
import { ref } from 'vue'
import Button from 'primevue/button'
defineProps({
  userData: Object,
})
document.title = 'app title'
</script>

<template>
      <p class="text-center text-base font-medium mb-4">白寿Payカードは持っていますか？</p>
    <div class="w-full max-w-xs bg-gray-100 rounded-lg p-4 mb-6">
      <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQoCViFCnLqddCN7uHZrEQ1u20IOBbAzvM4JA&s" class="w-full object-contain" />
    </div>
  <div class="w-full max-w-xs flex flex-col gap-4">
    <button @click="handleClickYes" class="w-full py-3 bg-blue-500 text-white rounded-full font-semibold text-base hover:bg-blue-600 transition">
      持っています
    </button>
    <button @click="handleClickNo" class="w-full py-3 border border-blue-500 text-blue-500 rounded-full font-semibold text-base hover:bg-blue-50 transition">
      持っていません
    </button>
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
