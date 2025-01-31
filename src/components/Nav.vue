<script>
import UiTypography from "../ui/UiTypography.vue";

export default {
  components: {
    UiTypography
  },
  data() {
    return {
      list: [ "Каталог", "Доставка", "Оплата", "Контакты", "О компании" ]
    };
  }
};
</script>

<template>
  <nav class="nav">
    <ul class="nav__list">
      <li class="nav__item" v-for="item, index in list" :key="index">
        <a class="nav__link" href="#">
          <UiTypography size="sm">{{ item }}</UiTypography>
        </a>
      </li>
    </ul>
  </nav>
</template>

<style>
.nav {
  display: flex;
}

.nav__list {
  list-style: none;
  display: flex;
  gap: 48px;
}

.nav__link {
  padding: 8px 0;
  text-decoration: none;
  color: var(--c-accent);

  &:hover {
    color: var(--c-accent-hover);
  }
}

@media screen and (max-width: 1200px) {
  .nav__list {
    gap: 36px;
  }
}

@media screen and (max-width: 992px) {
  .nav__list {
    padding: 24px 0;
    flex-direction: column;
    align-items: center;
    gap: 24px;
  }
}
</style>