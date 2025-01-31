<script>
import UiTypography from "../ui/UiTypography.vue";
import CatalogItem from "./CatalogItem.vue";

export default {
  components: {
    UiTypography,
    CatalogItem
  },

  emits: ['addToCart', 'removeFromCart'],

  props: {
    title: {
      type: String,
      required: true
    },
    items: {
      type: Array,
      required: true
    },
    cart: {
      type: Array,
      required: true
    }
  },

  methods: {
    handleAddToCart(id) {
      console.log('asd', id);
      this.$emit('addToCart', id);
    },

    handleRemoveFromCart(id) {
      console.log('asd', id);
      this.$emit('removeFromCart', id);
    }
  }
};
</script>

<template>
  <div class="catalog">
    <UiTypography tag="h1" size="xl" weight="bold">{{ title }}</UiTypography>
    <ul class="catalog__list">
      <li class="catalog__item" v-for="item in items" :key="item.id">
        <CatalogItem 
          :item="item"
          :inCart="cart.some(cartItem => cartItem === item.id)" 
          @addToCart="handleAddToCart" 
          @removeFromCart="handleRemoveFromCart"
        />
      </li>
    </ul>
  </div>
</template>

<style scoped>
.catalog {
  display: flex;
  flex-direction: column;
  gap: 40px;
}

.catalog__list {
  list-style: none;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 32px;
}

@media screen and (max-width: 1200px) {
  .catalog__list {
    grid-template-columns: repeat(3, 1fr);
  }
}

@media screen and (max-width: 992px) {
  .catalog__list {
    gap: 20px;
    grid-template-columns: repeat(2, 1fr);
  }
}

@media screen and (max-width: 600px) {
  .catalog__list {
    grid-template-columns: repeat(1, 1fr);
  }
}

</style>