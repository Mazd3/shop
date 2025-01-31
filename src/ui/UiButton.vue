<script>
export default {
  props: {
    selected: {
      type: Boolean,
    },
    loading: {
      type: Boolean,
    }
  },
  emits: ['click'],
};
</script>

<template>
  <button
    class="ui-button" 
    :class="{ 'ui-button--selected': selected }" 
    :disabled="loading" 
    @click="$emit('click')"
  >

    <template v-if="loading">
      <img class="ui-button__spinner" src="assets/spinner.svg" alt="loading">
    </template>

    <template v-if="selected" >
      <img class="ui-button__check" src="assets/check.svg" alt="check">
    </template>

    <slot />
   
  </button>
</template>

<style scoped>
.ui-button {
  outline: none;
  border: none;
  text-wrap: nowrap;

  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 4px;
  height: 48px;
  padding: 0 8px;

  background-color: var(--c-accent);
  color: var(--c-background);

  cursor: pointer;

  &:hover {
    background-color: var(--c-accent-hover);
  }
}

.ui-button__spinner {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: var(--c-accent-disabled);
}

.ui-button--selected {
  background-color: var(--c-accent-selected);
}

</style>

