<script>
import UiButton from "../ui/UiButton.vue";
import UiTypography from "../ui/UiTypography.vue";

export default {
  components: {
    UiTypography,
    UiButton
  },

  data() {
    return {
      value: ''
    }
  },

  methods: {
    handleSearch() {
      this.$emit('search', this.value);
    }
  }
};
</script>

<template>
  <div class="search">
    <input v-model="value" class="search__input" type="text" placeholder="Поиск по названию картины">
    <UiButton class="search__button" @click="handleSearch">
      <UiTypography class="search__button-text" size="sm" weight="bold">Найти</UiTypography>
    </UiButton>
  </div>
</template>

<style>
.search {
  display: flex;
  width: 100%;
  max-width: 400px;
}

.search__input {
  font-family: 'Merriweather', serif;
  font-size: 14px;
  width: 100%;
  padding: 0 16px;
  border: 1px solid var(--c-border);
  border-right: 0;
  outline: none;
  background: none;

  &:focus {
    border: 1px solid var(--c-border);
  }
  
  &::placeholder {
    color: #9F9F9F;
  }
}

.search__button {
  padding: 0 36px !important;
}


.search__button-text {
  color: var(--c-text-white) !important;
}

@media screen and (max-width: 992px) {
  .search__button {
  padding: 0 16px !important;
}
}


</style>