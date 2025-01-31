<script>
export default {
  props: {
    tag: {
      type: String,
      default: "span"
    },
    size: {
      type: String,
      default: 'md'
    },
    weight: {
      type: String,
      default: 'normal'
    },
  }
};
</script>

<template>
  <component :is="tag" class="ui-typography" :class="`${size} ${weight}`">
    <slot />
  </component>
</template>

<style scoped>
.ui-typography {
  font-family: "Merriweather", serif;
  font-weight: 400;
  font-style: normal;
}

.sm {
  font-size: 14px;
}

.md {
  font-size: 16px;
}

.lg {
  font-size: 18px;
}

.xl {
  font-size: 24px;
}

.bold {
  font-weight: bold;
}

.regular {
  font-weight: regular;
}
</style>