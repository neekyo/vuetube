<template>
  <div>
    <SearchBar @termChange="onTermChange">
    </SearchBar>
  </div>
</template>
  
<script>
import axios from 'axios';
import SearchBar from './components/SearchBar';
const API_KEY = ''

export default {
  name: "App",
  components: {
    SearchBar
  },
  methods: {
    async onTermChange(searchTerm) {
      const res = await axios.get('https://www.googleapis.com/youtube/v3/search', {
        params: {
          key: API_KEY,
          type: 'video',
          part: 'snippet',
          q: searchTerm
        }
      })
      return console.log(res);
    }
  }
};
</script>