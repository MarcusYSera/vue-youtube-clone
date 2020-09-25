<template>
  <div class="container">
    Hello World
    <!-- <SearchBar v-on:term-change="onTermChange"></SearchBar> -->
    <SearchBar @term-change="onTermChange"></SearchBar>
    <!-- <VideoList v-bind:videos="videos"></VideoList> -->
    <VideoList :videos="videos"></VideoList>
  </div>
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar';
import VideoList from './components/VideoList';
const API_KEY = 'AIzaSyBMPI6bM-QdSvWNVTXlhECFSZ-lWixYyGg';

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
          console.log(this.videos);
        });
    },
  },
};
</script>

<style></style>
