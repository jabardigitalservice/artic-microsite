<template>
  <div class="main-layout">
    <div class="content">
      <Nuxt />
    </div>
  </div>
</template>

<style>
html,
body {
  height: 100%;
}

body {
  background-color: #f7f7f7;
}

.main-layout > .content {
  max-width: 480px;
  width: 100%;
  background-color: #fff;
  margin: 0 auto;
}
</style>
