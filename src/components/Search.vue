<template>
  <input
    id="search"
    type="search"
    name="search"
    :value="value"
    @input="handleChange"
  />
</template>

<script>


export default {
  name: 'Search',
  props: {
    value: {
      type: String,
      required: true,
    }
  },
  methods: {
    handleChange(e) {
      this.$emit('input', e.target.value);
    }
  },
}
</script>

<style lang="scss">

.wrapper {
  margin: 0 auto;
  display: flex;
  box-sizing: border-box;
  width: 100%;
  padding: 30px;
  height: 100vh;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  input {
    display: flex;
    flex-direction: column;
    width: 300px;
    margin-top: 50px;
    background: none;
    height: 30px;
    border: 0;
    border-bottom: 1px solid #fff;
    outline: 0;
    color: #fff;
    transition: box-shadow .5s ease-in-out;
    &:focus {
      box-shadow: 0px 5px 10px -2px rgba(255,255,255,0.78);
   }
  }
}


</style>
