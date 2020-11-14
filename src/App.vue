<template>
  <div class="container">
    <h1>Youtube API</h1>
    <!-- <SearchBar v-on:term-change="onTermChange"></SearchBar> -->
    <SearchBar @term-change="onTermChange"></SearchBar>
    <div class="row" v-if="videos.length > 1">
      <VideoDetail v-bind:video="selectedVideo"></VideoDetail>
      <!-- <VideoList v-bind:videos="videos"></VideoList> -->
      <VideoList :videos="videos" v-on:video-select="onVideoSelect"></VideoList>
    </div>
    <h3 v-else class="textPrompt">Please Search for a Video to get Started</h3>
  </div>
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar';
import VideoList from './components/VideoList';
import VideoDetail from './components/VideoDetail';

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
            key: process.env.VUE_APP_API_KEY,
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

<style scoped>
.container {
  padding-top: 10px;
  min-height: 100vh;
  min-width: 100vw;
  background-image: linear-gradient(#09203f, #537895);
  color: white;
}
h1 {
  text-align: center;
}
.textPrompt {
  text-align: center;
}
</style>
