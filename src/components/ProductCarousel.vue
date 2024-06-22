<!-- src/components/ProductCarousel.vue -->
<template>
  <div class="recommend-container">
    <div class="recommend-header">
      <h2>Recommend</h2>
      <a href="#" class="see-all">See all</a>
    </div>
    <swiper :slides-per-view="4" space-between="20" class="recommend-content">
      <swiper-slide v-for="product in products" :key="product.id">
        <ProductCard :product="product" />
      </swiper-slide>
    </swiper>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import Swiper from 'swiper/bundle';
import 'swiper/css/bundle';
import ProductCard from './ProductCard.vue';

const products = ref([]);

// Загрузка данных из JSON
onMounted(async () => {
  const response = await fetch('/data/products.json');
  products.value = await response.json();
});
</script>

<style lang="scss">
.recommend-container {
  max-width: 1420px;
  margin: 0 auto;
  padding: 20px;

  .recommend-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;

    h2 {
      font-size: 24px;
      color: #ffffff;
    }

    .see-all {
      font-size: 16px;
      color: #00bcd4;
      text-decoration: none;
    }
  }

  .recommend-content {
    display: flex;
    gap: 20px;
  }
}
</style>
