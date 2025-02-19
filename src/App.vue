<script setup lang="ts">
import { ref } from 'vue'
import gsap from 'gsap'
const show = ref(true)
const show2 = ref(true)
const show3 = ref(true)

const onBeforeEnter = (el: Element) => {
  console.log('onBeforeEnter is called')
  gsap.set(el, {
    scaleX: 0.25,
    scaleY: 0.25,
    opacity: 1,
  })
}
const onEnter = (el: Element, done: () => void) => {
  console.log('onEnter is called')
  gsap.to(el, {
    duration: 1,
    scaleX: 1,
    scaleY: 1,
    opacity: 1,
    ease: 'elastic.inOut(2.5, 1)',
    onComplete: done,
  })
}
const onLeave = (el: Element, done: () => void) => {
  console.log('onLeave is called')
  gsap.to(el, {
    duration: 0.7,
    scaleX: 1,
    scaleY: 1,
    x: 300,
    ease: 'elastic.inOut(2.5, 1)',
  })
  gsap.to(el, {
    duration: 0.2,
    delay: 0.5,
    opacity: 0,
    onComplete: done,
  })
}
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

  <div>
    <button @click="show3 = !show3">Toggle</button>
    <Transition @before-enter="onBeforeEnter" @enter="onEnter" @leave="onLeave" :css="false">
      <div class="gsap-box" v-if="show3"></div>
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

.gsap-box {
  background: #42b883;
  margin-top: 20px;
  width: 30px;
  height: 30px;
  border-radius: 50%;
}
</style>
