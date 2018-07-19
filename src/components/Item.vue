<template>
  <div :style="style" class="photo" />
</template>

<script>
export default {
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      photo: this.item.links[0].href,
      title: this.item.data[0].title,
    };
  },
  computed: {
    style() {
      return `background: url("${this.photo}")`;
    },
  },
};
</script>

<style lang="scss">

.photo {
  width: 300px;
  height: 300px;
}

</style>
