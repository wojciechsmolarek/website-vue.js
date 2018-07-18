<template>
  <div class="search">
    <div class="wrapper">
      <Claim />
      <div class="search-bar">
        <input
          id="search"
          type="search"
          v-model="searchValue"
          @input='handleInput'
        />
      </div>
    </div>
  </div>
</template>

<script>

import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue'

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'Search',
  components: {
    Claim
  },
  data() {
    return {
      searchValue: '',
      results: [],
    };
  },
  methods: {
    //eslint-disable-next-line
    handleInput: debounce( function() {
      axios.get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
        })
        .catch(err => {
          console.log(err);
        })
    }, 500)
  }
};
</script>

<style lang="scss" scoped>
* {
  box-sizing: border-box;
}
body {
  font-family: sans-serif;
}
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
  font-family: sans-serif;
  background: url('../assets/hero-img.jpg') no-repeat 50% 0;
  background-size: cover;
  .search-bar {
    display: flex;
    flex-direction: column;
    width: 300px;
    input {
      margin-top: 50px;
      background: none;
      height: 30px;
      border: 0;
      border-bottom: 1px solid #111;
    }
  }
}

</style>
