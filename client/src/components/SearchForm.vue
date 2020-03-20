<template lang="html">
  <div>
    <div class="searchContainer">
      <div class="searchBox" @click="showSearchBar('artist')">Artist search</div>
      <div class="searchBox" @click="showSearchBar('album')">Album search</div>
      <div class="searchBox" @click="showSearchBar('track')">Track search</div>
    </div>
    <div class="searchBarContainer" v-if="!!searchType">
      <input v-model='searchValue' type="text" :placeholder="searchPlaceholder" @keyup="search">
    </div>
  </div>
</template>

<script>
import {eventBus} from '@/main.js';
export default {
  name: 'search-form',
  data() {
    return {
      searchValue: '',
      searchType: undefined,
      searchPlaceholder: '',

    }
  },
  methods: {
    showSearchBar: function(type) {

      this.searchType = type;
      this.searchPlaceholder = `Search for ${type}s`;
      this.searchValue = '';
    },
    search: function() {
      if (this.searchValue) {
        eventBus.$emit(`submit-${this.searchType}`, this.searchValue);
      }
    },
  }
}
</script>

<style lang="css" scoped>



</style>
