<template>
  <div class="product-page">
    <div class="product-page__header">
      <div class="product-page__gallery">
        <!-- Swiper Slider -->
        <Swiper :slides-per-view="1" loop="true" @swiper="onSwiperInit">
          <SwiperSlide v-for="(image, index) in images" :key="index">
            <img :src="image" alt="Slide image" />
          </SwiperSlide>
        </Swiper>

        <!-- Navigation Buttons -->
        <button class="prev-button" @click="slidePrev">Prev</button>
        <button class="next-button" @click="slideNext">Next</button>

        <!-- Thumbnails -->
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

      <!-- Product Information -->
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
    let swiper: any = null; // переменная для хранения экземпляра Swiper

    const onSwiperInit = (s: any) => {
      swiper = s; // сохраняем экземпляр Swiper
      swiper.on('slideChange', onSlideChange);
    };

    const onSlideChange = () => {
      if (swiper) {
        activeIndex.value = swiper.realIndex;
      }
    };

    const goToSlide = (index: number) => {
      if (swiper) {
        swiper.slideTo(index);
      }
    };

    const slidePrev = () => {
      if (swiper) {
        swiper.slidePrev();
      }
    };

    const slideNext = () => {
      if (swiper) {
        swiper.slideNext();
      }
    };

    return { product, images, activeIndex, goToSlide, slidePrev, slideNext, onSwiperInit };
  }
});
</script>

<style lang="scss" scoped>
/* Стили остаются без изменений */
</style>


<style lang="scss" scoped>
.product-page {
  margin-top: 25px;

  &__header {
    display: flex;
    justify-content: center;
  }

  &__gallery {
    position: relative;
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

    .prev-button, .next-button {
      position: absolute;
      top: 50%;
      transform: translateY(-50%);
      background-color: rgba(0, 0, 0, 0.5);
      color: #fff;
      border: none;
      padding: 10px;
      cursor: pointer;
      z-index: 10;
    }

    .prev-button {
      left: 10px;
    }

    .next-button {
      right: 10px;
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
