/*eslint linebreak-style: ["error", "windows"]*/
<template>
  <div class="wrapper">
    <h1>Bimberek :)</h1>
    <div class="search">
        <label for="search">Search: </label>
        <input id="search" name="search" v-model="searchValue" @input="handleImput"/>
        <ul>
            <li v-for="item in results" :key="item.data[0].nasa_id">
                <!-- <p>{{ item.data[0].description }}</p> -->
                <!-- {{ item.data[0].tittle }}
                {{ item.href }} -->
                <a v-bind:href="item.links[0].href">{{ item.data[0].title }}</a>
            </li>
        </ul>
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
        display: flex;
        flex-direction: column;
        align-items: center;
        margin: 0;
        padding: 30px;
        width: 100%
    }

    .search {
        display: flex;
        flex-direction: column;
        width: 300px
    }

    label {
        font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
    }

    input {
        height: 30px;
        border: 0;
        border-bottom: 1px solid black;
    }
</style>
