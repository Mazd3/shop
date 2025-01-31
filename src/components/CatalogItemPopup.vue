<script>
import UiPopup from "../ui/UiPopup.vue";
import UiTypography from "../ui/UiTypography.vue";
import UiButton from "../ui/UiButton.vue";
import UiSlider from "../ui/UiSlider.vue";

export default {
  components: {
    UiPopup,
    UiTypography,
    UiButton,
    UiSlider
  },
  emits: ['close', 'cartButton'],
  props: {
    item: {
      type: Object,
      required: true
    },
    inCart: {
      type: Boolean,
      default: false
    },
    isLoading: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    formattedPrice() {
      return this.item.price.toLocaleString('ru-RU');
    },
    formattedOldPrice() {
      if (!this.item.oldPrice) {
        return undefined;
      }
      return this.item.oldPrice.toLocaleString('ru-RU');
    }
  }
};
</script>

<template>
  <UiPopup @close="$emit('close')">
    <div class="popup" :class="{ 'popup--sold': item.sold }">

      <UiSlider class="popup__slider" :images="item.images" />

      <UiTypography size="lg" weight="bold">{{ item.title }}</UiTypography>
      <UiTypography size="md">{{ item.description }}</UiTypography>

      <template v-if="item.sold">
          <UiTypography class="item__sold" size="md">Продана на аукционе</UiTypography>
        </template>

      <div v-else class="popup__buy">

        <div class="popup__price-wrapper">
          <UiTypography v-if="item.oldPrice" class="popup__old-price" size="sm">{{ formattedOldPrice }} $</UiTypography>
          <UiTypography class="popup__price" size="md" weight="bold">{{ formattedPrice }} $</UiTypography>
        </div>

        <UiButton class="popup__button" :selected="inCart" @click="$emit('cartButton')" :loading="isLoading">
          <UiTypography class="popup__button-text" size="sm" weight="bold">{{ inCart ? 'В корзине' : 'Купить' }}</UiTypography>
        </UiButton>
      </div>
    </div>
  </UiPopup>
</template>

<style scoped>
.popup {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.popup--sold {
  opacity: 0.5;
}

.popup__buy {
  display: flex;
  gap: 16px;
  align-items: center;
  justify-content: space-between;
}

.popup__price-wrapper {
  display: flex;
  flex-direction: column;
}

.popup__old-price {
  text-decoration: line-through;
  color: #C1B4B1;
}

.popup__button {
  padding: 0 16px;
}

.popup__button-text {
  color: var(--c-background);
}
</style>