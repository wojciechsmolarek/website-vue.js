<template>
  <div class="heroImg" />
</template>

<script>
export default {
}
</script>

<style lang="scss">
.heroImg {
  position: fixed;
  width: 100%;
  height: 100vh;
  z-index: -1;
  background: url('../assets/hero-img.jpg') no-repeat 50% 0;
  background-size: cover;
  &::after {
    content: '';
    position: absolute;
    z-index: 1;
    width: 100%;
    height: 100vh;
    background: rgba(0,0,0,.4);
  }
}
</style>
