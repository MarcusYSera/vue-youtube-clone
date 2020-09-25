<template>
  <div class="container">
    Hello World
    <!-- <SearchBar v-on:term-change="onTermChange"></SearchBar> -->
    <SearchBar @term-change="onTermChange"></SearchBar>
    <div class="row">
      <VideoDetail v-bind:video="selectedVideo"></VideoDetail>
      <!-- <VideoList v-bind:videos="videos"></VideoList> -->
      <VideoList :videos="videos" v-on:video-select="onVideoSelect"></VideoList>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar';
import VideoList from './components/VideoList';
import VideoDetail from './components/VideoDetail';
const API_KEY = 'AIzaSyBMPI6bM-QdSvWNVTXlhECFSZ-lWixYyGg';

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
      // console.log(this.selectedVideo);
    },
    onTermChange(searchTerm) {
      axios
        .get('https://www.googleapis.com/youtube/v3/search', {
          params: {
            key: API_KEY,
            type: 'video',
            part: 'snippet',
            q: searchTerm,
          },
        })
        .then(res => {
          this.videos = res.data.items;
          // console.log(this.videos);
        });
    },
  },
};
</script>

<style></style>
