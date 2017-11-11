<template>
  <div class="container" id="app">
    <source-selection v-on:sourceChanged="sourceChanged"></source-selection>
    <news-list v-bind:source="source"></news-list>  
  </div>
</template>

<script>

import SourceSelection from './components/SourceSelection';
import NewsList from './components/NewsList';

export default {
  name: 'app',
  components: {
    'source-selection': SourceSelection,
    'news-list': NewsList,
  },
  data() {
    return {
      source: "",
    }
  },
  methods: {
    sourceChanged: function(source) {
      this.source = source;
    }
  }
}
</script>

<style>
#app {
  padding-top: 20px;
}
</style>
