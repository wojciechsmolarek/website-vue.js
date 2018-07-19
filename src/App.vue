<template>
  <div :class="[{flexStart: step === 1}, 'wrapper']">
    <transition name="fade">
      <HeroImg v-if="step === 0" />
    </transition>
    <Claim v-if="step === 0" />
    <Search v-model="searchValue" @input="handleInput" :dark="step === 1"/>
    <div class="results" v-if="results && !loading && step === 1">
      <Item v-for="item in results" :item="item" :key="item.data[0].nasa_id"/>
    </div>
  </div>
</template>

<script>

import Claim from '@/components/Claim.vue';
import Search from '@/components/Search.vue';
import HeroImg from '@/components/HeroImg.vue';
import Item from '@/components/Item.vue';

import axios from 'axios';
import debounce from 'lodash.debounce';

const API = 'https://images-api.nasa.gov/search';



export default {
  components: {
    Claim,
    Search,
    HeroImg,
    Item,
  },
  data() {
    return {
      loading: false,
      step: 0,
      searchValue: '',
      results: [],
    };
  },
  methods: {
    //eslint-disable-next-line
    handleInput: debounce( function() {
      this.loading = true;
      axios.get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.step = 1;
          this.loading = false;
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

.fade-enter-active, .fade-leave-active {
  transition: opacity .4s ease;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}

.results {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-gap: 20px;

  @media screen and (max-width: 988px) {
    grid-template-columns: 1fr 1fr;
  }
   @media screen and (max-width: 650px) {
      grid-template-columns: 1fr;
    }
}

</style>
