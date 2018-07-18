<template>
  <div class="wrapper">
    <Claim />
    <Search v-model="searchValue" @input="handleInput" />
    <HeroImg />
  </div>
</template>

<script>

import Claim from '@/components/Claim.vue';
import Search from '@/components/Search.vue';
import HeroImg from '@/components/HeroImg.vue';

import axios from 'axios';
import debounce from 'lodash.debounce';

const API = 'https://images-api.nasa.gov/search';



export default {
  components: {
    Claim,
    Search,
    HeroImg,
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
          console.log(this.searchValue);
        })
        .catch(err => {
          console.log(err);
        })
    }, 500)
  }
};

</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Montserrat:300,400,700');

* {
  box-sizing: border-box;
}
body {
  color: #fff;
  font-family: 'Montserrat', sans-serif;
  font-weight: lighter;

}

</style>
