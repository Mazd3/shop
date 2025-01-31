<script>
import UiTypography from "../ui/UiTypography.vue";
import UiButton from "../ui/UiButton.vue";
import CatalogItemPopup from "./CatalogItemPopup.vue";

export default {
  components: {
    UiTypography,
    UiButton,
    CatalogItemPopup
  },

  data() {
    return {
      isLoading: false,
      showPopup: false,
    }
  },

  emits: ['addToCart', 'removeFromCart'],

  props: {
    item: {
      type: Object,
      required: true
    },
    inCart: {
      type: Boolean,
      default: false
    },
  },

  methods: {
    handleCartButton() {
      if (this.inCart) {
        this.isLoading = true;
        setTimeout(() => {
          this.$emit('removeFromCart', this.item.id);
          this.isLoading = false;
        }, 2000);
      } else {
        this.isLoading = true;
        setTimeout(() => {
          this.$emit('addToCart', this.item.id);
          this.isLoading = false;
        }, 2000);
      }
    },

    handleShowPopup() {
      this.showPopup = true;
    },

    handleClosePopup() {
      this.showPopup = false;      console.log('qwe', id);
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

  <div class="item__wrapper">

  <CatalogItemPopup v-if="showPopup" :item="item" :inCart="inCart" @close="handleClosePopup" @cartButton="handleCartButton" :isLoading="isLoading" />

    <div class="item" :class="{ 'item--sold': item.sold }">

      <img class="item__image" :src="item.images[0]" :alt="item.title" @click="handleShowPopup">
      <div class="item__main">

        <div class="item__title" @click="handleShowPopup">
          <UiTypography  size="lg">{{ item.title }}</UiTypography>
        </div>

        <div class="item__buy">

          <template v-if="item.sold">
            <UiTypography class="item__sold" size="md">Продана на аукционе</UiTypography>
          </template>

          <template v-else>
            <div class="item__price-wrapper">
              <UiTypography v-if="item.oldPrice" class="item__old-price" size="sm">{{ formattedOldPrice }} $</UiTypography>
              <UiTypography class="item__price" size="md" weight="bold">{{ formattedPrice }} $</UiTypography>
            </div>
            <UiButton class="item__button" :loading="isLoading" :selected="inCart" @click="handleCartButton">
              <UiTypography class="item__button-text" size="sm" weight="bold">{{ inCart ? 'В корзине' : 'Купить' }}</UiTypography>
            </UiButton>
          </template>

        </div>

      </div>
    </div>
  </div>
</template>

<style scoped>
.item__wrapper {
  height: 100%;
}

.item {
  display: flex;
  flex-direction: column;
  border: 1px solid #E1E1E1;
  height: 100%;
}

.item--sold {
  opacity: 0.5;
}

.item__image {
  cursor: pointer;
  width: 100%;
  object-fit: cover;
  aspect-ratio: 16/9;
}

.item__main {
  flex: 1;
  padding: 24px;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.item__title {
  cursor: pointer;
}

.item__buy {
  flex: 1;
  display: flex;
  align-items: center;
  gap: 12px;
}

.item__price-wrapper {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.item__price {
  text-wrap: nowrap;
}

.item__sold {
  grid-column: span 2;
  grid-row: 2;
}

.item__old-price {
  text-decoration: line-through;
  color: #A0A0A0
}

.item__button {
  flex: 1;
}

.item__button-text {
  color: #fff;
}

</style>