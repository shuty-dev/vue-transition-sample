<script setup lang="ts">
import { ref } from 'vue'
const show = ref(true)
const show2 = ref(true)
</script>

<template>
  <div>
    <button @click="show = !show">Toggle</button>
    <Transition>
      <p v-if="show">hello</p>
    </Transition>
  </div>
  <div>
    <button @click="show2 = !show2">Toggle2</button>
    <Transition name="hogehoge">
      <p v-if="show2">hello</p>
    </Transition>
  </div>
</template>

<style scoped>
.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}

.hogehoge-enter-active {
  transition: all 0.3s ease-out;
}

.hogehoge-leave-active {
  transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
}

.hogehoge-enter-from,
.hogehoge-leave-to {
  transform: translateX(20px);
  opacity: 0;
}
</style>
