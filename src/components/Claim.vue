<template>
  <div class="claim-wrapper">
    <h1 class="claim">SPACE</h1>
    <p class="subClaim">Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud.</p>
    <p class="subClaim">Sunt in culpa qui officia deserunt mollit anim id est laborum.</p>

  </div>

</template>

<script>
export default {
}
</script>

<style lang="scss">
body {
  margin: 0;
}
.claim-wrapper {
  width: 50%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  @media screen and (max-width: 536px) {
    width: 100%;
  }
}
.claim {
  font-size: 50px;
  font-weight: 700;
}
.subClaim {
  font-size: 15px;
}

</style>
