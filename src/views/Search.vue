<template>
  <div class="search">
    <div class="wrapper">
      <div class="search-bar">
        <label for="search">Search</label>
        <input
          id="search"
          type="search"
          v-model="searchValue"
          @input='handleInput'
        />
        <ul>
          <li v-for="item in results" :key="item.data[0].nasa_id">
            <p>{{ item.data[0].description }}</p>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>

import axios from 'axios';
import debounce from 'lodash.debounce';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'Search',
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

<style lang="scss">
.wrapper {
  margin: 0 auto;
  display: flex;
  width: 100%;
  padding: 30px;
  height: 100vh;
  flex-direction: column;
  align-items: center;
  font-family: sans-serif;
  .search-bar {
    display: flex;
    flex-direction: column;
    width: 300px;
    input {
      height: 30px;
      border: 0;
      border-bottom: 1px solid #111;
    }
  }
}

</style>
