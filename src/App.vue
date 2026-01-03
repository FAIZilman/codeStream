<script setup>
import { onMounted, ref, reactive, onUnmounted } from 'vue';
import LayoutNavbar from './components/layout/LayoutNavbar.vue';
import SectionHero from './components/sections/SectionHero.vue';
import SectionAbout from './components/sections/SectionAbout.vue';
import SectionWhyUs from './components/sections/SectionWhyUs.vue';
import SectionFaq from './components/sections/SectionFaq.vue';
import AOS from 'aos';
// import { useStorage } from '@vueuse/core';
import 'aos/dist/aos.css';
import SectionFooter from './components/sections/SectionFooter.vue';

let darkModeStorage = ref(JSON.parse(localStorage.getItem('darkMode')) ?? window.matchMedia("(prefers-color-scheme : dark)").matches);
function callback() {
  darkModeStorage.value = !darkModeStorage.value;
  localStorage.setItem('darkMode', darkModeStorage.value);
}

let mouseX = ref(0)
let mouseY = ref(0)

let trails = reactive([]);


function animate() {
  let target = {
    x: mouseX.value,
    y: mouseY.value
  }

  trails.forEach((trail) => {
    trail.x += (target.x - trail.x) * 0.65;
    trail.y += (target.y - trail.y) * 0.65
    target = trail
  });

  requestAnimationFrame(animate)
}


onMounted(() => {
  let cursorPointer = document.getElementById('cursor-pointer');

  function createTrails(jmlhTrail) {
    for (let i = 0; i < jmlhTrail; i++) {
      let div = document.createElement('div');
      div.classList.add('trail')
      trails.push({
        x: mouseX.value,
        y: mouseY.value
      })
    }
  }

  const onMouseMove = (e) => {
    mouseX.value = e.clientX;
    mouseY.value = e.clientY

    cursorPointer.style.left = mouseX.value + 'px'
    cursorPointer.style.top = mouseY.value + 'px'
  }

  createTrails(8)

  window.addEventListener('mousemove', onMouseMove);

  animate()

  window.addEventListener('mousedown', () => {
    cursorPointer.classList.add('scale-130');
  })

  window.addEventListener('mouseup', () => {
    cursorPointer.classList.remove('scale-130');
  })

  onUnmounted(() => {
    window.removeEventListener('mousemove', onMouseMove)
  })

  AOS.init({
    duration: 600,
    easing: 'ease-in-out',
    once: true,
    offset: 100
  })
});
</script>

<template>
  <div :class="darkModeStorage ? 'dark' : 'light'" class="cursor-none">
    <!-- shadow-[10px 10px 10px 0px rgba(0,500,0,.2)] -->
    <div
      class="fixed w-5 h-5 rounded-full dark:bg-white bg-[#28282a] -translate-1/2 z-[999] transition pointer-events-none darkTrailLeader dark:trailLeader"
      id="cursor-pointer">
    </div>
    <div v-for="(trail, i) in trails" :key="i" class="trail bg-[#28282a] dark:bg-white" :style="{
      left: trail.x + 'px',
      top: trail.y + 'px',
      opacity: (trails.length - i) / trails.length,
    }"></div>
    <LayoutNavbar :dark-mode="darkModeStorage" @darkEvent="callback" />
    <SectionHero />
    <SectionAbout />
    <SectionWhyUs />
    <SectionFaq />
    <SectionFooter />
  </div>
</template>

<style scoped>
.darkTrailLeader {
  box-shadow: 0 0 15px rgba(9, 9, 9, 0.5);
}



.trail {
  position: fixed;
  pointer-events: none;
  width: 14px;
  height: 14px;
  transform: translate(-50%, -50%);
  border-radius: 100%;
  z-index: 9999;
}
</style>
<!-- transition: transform 0.1s ease-out, opacity 0.3s ease-out; -->
