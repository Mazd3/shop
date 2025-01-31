<script>
export default {
  emits: ['close'],
  methods: {
    handleClose() {
      this.$emit('close');
    },
  }
};
</script>

<template>
    <div class="ui-popup__wrapper" @click.self="handleClose">
      <div class="ui-popup">
        <slot />
      </div>
    </div>
</template>

<style scoped>
.ui-popup__wrapper {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 100;
}

.ui-popup {
  max-width: calc(min(100vw - 40px, 800px));
  background-color: var(--c-background);
  padding: 24px;
}
</style>