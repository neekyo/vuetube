<template>
  <div class="body">
    <div>
      <h4 class="header">
        <i class="devicon-vuejs-plain colored" />
        <span>VueTube</span>
      </h4>
      <SearchBar @termChange="onTermChange"></SearchBar>
      <div class="row color">
        <VideoDetail :video="selectedVideo" />
        <VideoList @videoSelect="onVideoSelect" :videos="videos"></VideoList>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar';
import VideoList from './components/VideoList';
import VideoDetail from './components/VideoDetail';

const API_KEY = 'AIzaSyBGRaNMkaxtz43Xi2DL0YT9w4m_-FoALz4';

export default {
  name: 'App',
  components: {
    SearchBar,
    VideoList,
    VideoDetail,
  },
  data() {
    return { videos: [], selectedVideo: null };
  },
  methods: {
    onVideoSelect(video) {
      this.selectedVideo = video;
    },
    async onTermChange(searchTerm) {
      const res = await axios.get(
        'https://www.googleapis.com/youtube/v3/search',
        {
          params: {
            key: API_KEY,
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

<style>
.body {
  background-color: #000;
  height: 100vh;
  color: #fff;
  padding: 0 2rem 0 2rem;
}
.header {
  padding: 0.5rem 0 0.5rem 1rem;
  background-color: #202020;
}
.header span {
  color: #fff;
  font-size: 15px;
}
.header i {
  padding-right: 0.25rem;
  vertical-align: middle;
}
</style>
