<template>
  <div class="top-section"></div>
  <div class="content-container">
    <div class="content">
      <slot></slot>
    </div>
    <div class="left-nav">
      <i class="fas fa-th-large"></i>
      <i class="fas fa-tag"></i>
      <i class="fas fa-chart-bar"></i>
      <i class="fas fa-cog"></i>
    </div>
  </div>
</template>
<script>
export default {
  data() {

  }
}
</script>
<style scoped lang="scss">
@import "style/layout.scss";
</style>