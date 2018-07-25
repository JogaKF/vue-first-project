/*eslint linebreak-style: ["error", "windows"]*/
<template>
  <div class="wrapper">
        <Claim />
        <SearchImput />
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchImput from '@/components/SearchImput.vue';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'Search',

  components: {
    Claim,
    SearchImput,
  },

  data() {
    return {
      searchValue: ' ',
      results: [],
    };
  },

  methods: {// eslint-disable-next-line
    handleImput: debounce(function () {
      axios.get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
          console.log(this.results);
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),
  },
};
</script>

<style lang="scss" scoped>
    .wrapper {
        margin: 0;
        padding: 30px;
        width: 100%;
        height: 100vh;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        background-image: url('../assets/backgrundSearch.jpg');
        background-repeat: no-repeat;
        background-size: cover;
        background-position: center;
    }
</style>
