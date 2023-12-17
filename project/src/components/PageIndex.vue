<template>
  <preloader />

  <!-- page wrap
    ================================================== -->
  <div id="page" class="s-pagewrap ss-home">
    <page-index-header />
    <page-index-content />
    <page-index-footer />
  </div>
</template>
    
<script setup>
import Preloader from "@/components/Preloader.vue";
import PageIndexHeader from "@/components/PageIndexHeader.vue";
import PageIndexContent from "@/components/PageIndexContent.vue";
import PageIndexFooter from "@/components/PageIndexFooter.vue";
</script>