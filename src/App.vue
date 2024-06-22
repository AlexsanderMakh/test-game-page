<template>
  <div id="app">
    <ProductPage />
    <SwiperComponent/>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import ProductPage from './components/ProguctPage.vue';
import SwiperComponent from "./components/SwiperComponent.vue";



export default defineComponent({
  name: 'App',
  components: {
    SwiperComponent,
    ProductPage,
  },
});
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #ffffff;
  margin-top: 60px;
  background-color: #01081e;
}

</style>
