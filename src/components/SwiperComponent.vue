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

<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { Swiper, SwiperSlide } from 'swiper/vue';
import 'swiper/scss';
import 'swiper/scss/navigation';
import 'swiper/scss/pagination';
import ProductCard from './ProductCard.vue';

interface Product {
  id: number;
  name: string;
  image: string;
  tags: string[];
  isNew: boolean;
  isHot: boolean;
  downloads: string;
}

const products = ref<Product[]>([]);

onMounted(async () => {
  const response = await fetch('/data/products.json');
  products.value = await response.json();
});
</script>

<style lang="scss">

</style>
