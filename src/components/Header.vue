<script>
import Nav from "./Nav.vue";
import Search from "./Search.vue";
import UiButton from "../ui/UiButton.vue";

export default {
  components: {
    Nav,
    Search,
    UiButton
  },

  data() {
    return {
      isOpen: false
    }
  },

  emits: ['search'],

  methods: {
    handleBurger() {
      this.isOpen = !this.isOpen
    },
    handleSearch(value) {
      this.$emit('search', value);
    }
  }
};
</script>

<template>
  <div class="header">
    <UiButton class="header__burger" @click="handleBurger" >{{ isOpen ? 'x' : '='  }}</UiButton>
    <Nav class="header__nav" :class="{ 'header__nav--open': isOpen }" />
    <Search class="header__search" @search="handleSearch" />
  </div>
</template>

<style>
.header {
  height: 100%;
  margin: 0 auto;
  max-width: var(--content-width);
  padding: 0 20px;
  display: flex;
  gap: 32px;
  align-items: center;
  justify-content: center;
}

.header__nav {
  flex: 1;
  justify-content: center;
}

.header__burger {
  aspect-ratio: 1/1;
  display: none !important;
}

@media screen and (max-width: 992px) {
  .header {
    z-index: 100;
    gap: 20px;
    justify-content: space-between;
  }

  .header__burger {
    display: block !important;
  }

  .header__nav {
    display: none;
  }

  .header__nav--open {
    display: flex !important;
    position: fixed;
    top: 96px;
    left: 0;
    bottom: 0;
    width: 100%;
    background-color: var(--c-background);
    z-index: 1;
  }
}

</style>