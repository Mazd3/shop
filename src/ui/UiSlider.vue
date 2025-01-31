<script>
import UiButton from './UiButton.vue';

export default {

  components: {
    UiButton
  },

  props: {
    images: {
      type: Array,
      required: true
    }
  },

  data() {
    return {
      current: 0
    }
  },

  methods: {
    nextImage() {
      this.current = (this.current + 1) % this.images.length
    },
    prevImage() {
      this.current = (this.current - 1 + this.images.length) % this.images.length
    }
  }
};
</script>

<template>
  <div class="slider__wrapper">
    <div class="slider">
      <img class="slider__image" :src="images[current]" alt="image">
    </div>
    <div class="slider__controls">
      <UiButton class="slider__button" @click="prevImage"><</UiButton>
      <UiButton class="slider__button" @click="nextImage">></UiButton>
    </div>
  </div>
</template>

<style scoped>
.slider__wrapper {
  position: relative;
}

.slider {
  position: relative;
  width: 100%;
  aspect-ratio: 16/9;
}

.slider__image {
  position: absolute;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.slider__controls {
  position: absolute;
  top: 50%;
  width: 100%;
  transform: translateY(-50%);
  display: flex;
  justify-content: space-between;
}

.slider__button {
  width: 48px;
  height: 48px;
}
</style>