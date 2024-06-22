<template>
  <div class="product-page">
    <div class="product-page__header">
      <div class="product-page__gallery">
        <Swiper ref="swiperRef" :slides-per-view="1" loop="true" @slideChange="onSlideChange">
          <SwiperSlide v-for="(image, index) in images" :key="index">
            <img :src="image" alt="Slide image" />
          </SwiperSlide>
        </Swiper>
        <div class="product-page__thumbnails">
          <img
              v-for="(image, index) in images"
              :key="index"
              :src="image"
              alt="Thumbnail image"
              :class="{ 'active-thumbnail': index === activeIndex }"
              @click="goToSlide(index)"
          />
        </div>
      </div>
      <div class="product-page__info">
        <h1 class="product-page__title">{{ product.title }}</h1>
        <p class="product-page__description">{{ product.description }}</p>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted } from 'vue';
import { Swiper, SwiperSlide } from 'swiper/vue';
import 'swiper/swiper-bundle.css';
import slide1 from '../assets/images/1-slide.png';
import slide2 from '../assets/images/2-slide.png';
import slide3 from '../assets/images/3-slide.png';
import slide4 from '../assets/images/4-slide.png';

interface Product {
  title: string;
  description: string;
}

export default defineComponent({
  name: 'ProductPage',
  components: { Swiper, SwiperSlide },
  setup() {
    const product = ref<Product>({
      title: 'Modification name',
      description: 'Description: Are you ready to embark on the wildest bureaucratic adventure of your life, do you have a passion for enforcing regulations that nobody asked for: Then buckle up, because the Bureau of Land Mismanagement is looking for its next Ranger to join our illustrious team of paper-pushing eco-warriors!'
    });
    const images = ref<string[]>([slide1, slide2, slide3, slide4]);
    const activeIndex = ref(0);
    const swiperRef = ref<any>(null);

    const onSlideChange = (swiper: any) => {
      activeIndex.value = swiper.realIndex;
    };

    const goToSlide = (index: number) => {
      if (swiperRef.value && swiperRef.value.swiper) {
        swiperRef.value.swiper.slideTo(index);
        activeIndex.value = index;
      }
    };

    onMounted(() => {
      if (swiperRef.value && swiperRef.value.swiper) {
        swiperRef.value.swiper.on('slideChange', onSlideChange);
      }
    });

    return { product, images, activeIndex, onSlideChange, goToSlide, swiperRef };
  }
});
</script>

<style lang="scss" scoped>
.product-page {
  margin-top: 25px;
  &__header {
    display: flex;
    justify-content: center;
  }

  &__gallery {
    width: 694px;
    height: 515px;
    margin-right: 40px;



    .swiper-slide {
      display: flex;
      justify-content: center;
      align-items: center;

    }

    img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      border-radius: 15px;
    }
  }

  &__thumbnails {
    display: flex;
    justify-content: center;
    margin-top: 10px;

    img {
      width: 175px;
      height: 100px;
      object-fit: cover;
      cursor: pointer;
      border: 2px solid transparent;
    }

    .active-thumbnail {
      border: 2px solid #007aff;
    }
  }

  &__info {
    width: 694px;
    height: 515px;
    text-align: left;
    margin-top: 70px;
  }

  &__title {
    font-size: 46px;
    font-weight: bold;
  }

  &__description {
    margin-top: 10px;
    font-size: 24px;
    font-family: Yantramanav, sans-serif;
    font-weight: 400;
    line-height: 32px;
  }
}
</style>
