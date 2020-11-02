<template>
  <div class="container">
    <SearchBar @termChange="onTermChange"> </SearchBar>
    <VideoList :videos="videos"></VideoList>
  </div>
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar';
import VideoList from './components/VideoList';

export default {
  name: 'App',
  components: {
    SearchBar,
    VideoList,
  },
  data() {
    return { videos: [] };
  },
  methods: {
    async onTermChange(searchTerm) {
      const res = await axios.get(
        'https://www.googleapis.com/youtube/v3/search',
        {
          params: {
            key: process.env.VUE_APP_YOUTUBE_API_KEY,
            type: 'video',
            part: 'snippet',
            q: searchTerm,
          },
        }
      );
      this.videos = res.data.items;
    },
  },
};
</script>
