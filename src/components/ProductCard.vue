<template>
  <div class="product-card">
    <img :src="product.image" alt="Product Image" class="product-card__image" />
    <div class="product-card__tags">
      <span v-for="tag in product.tags" :key="tag" class="product-card__tag">{{ tag }}</span>
    </div>
    <div class="product-card__badges">
      <span v-if="product.isNew" class="product-card__badge product-card__badge--new"></span>
      <span v-if="product.isHot" class="product-card__badge product-card__badge--hot"></span>
    </div>
    <div class="product-card__info">
      <span class="product-card__downloads">{{ product.downloads }} downloads</span>
      <button class="product-card__save-btn" @click="toggleFavorite">
        {{ isFavorite ? '💖' : '⭐' }}
      </button>
    </div>
    <h3 class="product-card__name">{{ product.name }}</h3>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { defineProps } from 'vue';

interface Product {
  id: number;
  name: string;
  image: string;
  tags: string[];
  isNew: boolean;
  isHot: boolean;
  downloads: string;
}

const props = defineProps<{
  product: Product;
}>();
// Добавляем состояние для отслеживания, находится ли продукт в избранном
const isFavorite = ref(false);

// Функция для переключения состояния избранного
const toggleFavorite = () => {
  isFavorite.value = !isFavorite.value;
};
</script>

<style lang="scss" scoped>
.product-card {
  position: relative;
  width: 100%;
  max-width: 300px;
  border-radius: 10px;
  padding: 15px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);

  &__image {
    width: 100%;
    height: auto;
    border-radius: 10px;
  }

  &__tags {
    position: absolute;
    top: 10px;
    display: flex;
    flex-wrap: wrap;
    gap: 5px;
  }

  &__tag {
    background-color: #333;
    color: #fff;
    padding: 5px;
    border-radius: 3px;
    font-size: 12px;
  }

  &__badges {
    position: absolute;
    top: 10px;
    right: 1px;
    display: flex;
    flex-direction: column;
    gap: 5px;
  }

  &__badge {
    width: 80px; /* Adjust to your image size */
    height: 50px; /* Adjust to your image size */
    background-size: contain;
    background-repeat: no-repeat;
    background-position: center;
    position: relative;

    &--new {
      background-image: url('../assets/images/up_image/New.png');
    }
    &--hot {
      background-image: url('../assets/images/up_image/Hot.png');
    }
  }

  &__info {
    display: flex;
    justify-content: space-between;
    align-items: center;
    position: absolute;
    bottom: 62px;
    left: 15px;
    right: 15px;
    color: white;
    background: rgba(0, 0, 0, 0.5);
    padding: 5px 10px;
    border-radius: 6px;
  }

  &__downloads {
    font-size: 14px;
  }

  &__save-btn {
    background: none;
    border: none;
    cursor: pointer;
    font-size: 20px;
    color: white; /* Меняем цвет звезды на белый */
  }

  &__save-btn--active {
    color: red; /* Меняем цвет на красный, когда добавлено в избранное */
  }

  &__name {
    margin-top: 10px;
    font-size: 18px;
    font-weight: bold;
  }
}
</style>
