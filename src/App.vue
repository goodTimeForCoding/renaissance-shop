<template>
  <div id="app">
    <HeaderComponent @search="searchQuery = $event"/>
    <main class="main-content">
      <GalleryComponent :searchQuery="searchQuery" />
    </main>
    <FooterComponent />
  </div>
</template>

<script>
import HeaderComponent from '@/components/HeaderComponent/index.vue';
import GalleryComponent from '@/components/GalleryComponent/index.vue';
import FooterComponent from '@/components/FooterComponent/index.vue';

export default {
  components: {
    HeaderComponent,
    GalleryComponent,
    FooterComponent,
  },
  data() {
    return {
      searchQuery: '',
    };
  },
};
</script>

<style scoped>
#app {
  display: grid;
  grid-template-rows: auto 1fr auto;
  height: 100vh;
}
</style>
