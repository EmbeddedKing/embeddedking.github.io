<template>
  <!-- preloader
    ================================================== -->
  <div id="preloader">
    <div id="loader" class="dots-fade">
      <div></div>
      <div></div>
      <div></div>
    </div>
  </div>
</template>

<script setup>
import { onMounted } from "vue";

const html = document.documentElement

onMounted(() => {
  const ssPreloader = function () {
    const siteBody = document.querySelector('body');
    const preloader = document.querySelector('#preloader');
    if (!preloader) return;

    html.classList.add('ss-preload');

    window.addEventListener('load', function () {
      html.classList.remove('ss-preload');
      html.classList.add('ss-loaded');

      preloader.addEventListener('transitionend', function afterTransition(e) {
        if (e.target.matches('#preloader')) {
          // siteBody.classList.add('ss-show');
          e.target.style.display = 'none';
          preloader.removeEventListener(e.type, afterTransition);
        }
      });
    });
  }; // end ssPreloader
  ssPreloader()
})
</script>