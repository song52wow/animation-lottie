<script setup>
import { onMounted, ref } from 'vue';
import lottie from 'lottie-web'
import {gsap} from 'gsap'
import {ScrollTrigger} from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const baseURL = import.meta.env.BASE_URL

const mainRef = ref()
const lottieRef = ref()

onMounted(() => {
  const lottieAnimation = lottie.loadAnimation({
    container: lottieRef.value,
    renderer: 'svg',
    loop: false,
    autoplay: false,
    path: baseURL + '/bloom.json'
  });

  ScrollTrigger.create({
    trigger: mainRef.value,
    start: 'top top',
    end: 'bottom bottom',
    scrub: true,
    pin: true,
    onUpdate(self) {
      lottieAnimation.goToAndStop(self.progress * lottieAnimation.totalFrames, true)
    } 
  })
})
</script>

<template>
  <main ref="mainRef">
    <div class="lottie" ref="lottieRef"></div>
  </main>
</template>

<style scoped>
main {
  height: 200vh;
}

.lottie {
  width: 800px;
}
</style>
