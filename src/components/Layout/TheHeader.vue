<template>
  <header class="header">
    <h1 class="title">calc</h1>
    <BaseThemeControl />
  </header>
</template>

<style lang="scss" scoped>
.header {
  @include flex(1rem);
  align-items: center;
  justify-content: space-between;
  padding-left: 0.5rem;
}

h1 {
  margin: 0;
}

.title {
  font-size: $fs;
  color: var(--text-header);
}
</style>
