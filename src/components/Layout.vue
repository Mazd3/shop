<template>
  <div class="layout">
    <header class="layout__header">
      <slot name="header" />
    </header>

    <main class="layout__main">
      <slot name="main" />
    </main>

    <footer class="layout__footer">
      <slot name="footer" />
    </footer>
  </div>
</template>

<style scoped>
.layout {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.layout__header {
  z-index: 100;
  position: sticky;
  top: 0;
  height: 96px;
  background-color: var(--c-background);
  border-bottom: 1px solid #E1E1E1;
}

.layout__main {
  margin: 0 auto;
  padding: 45px 20px;
  max-width: var(--content-width);
  width: 100%;
  flex: 1 0 auto;
}

.layout__footer {
  height: 96px;
  background-color: #ECEAEA;
}

</style>