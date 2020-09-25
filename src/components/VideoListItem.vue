<template>
  <li class="list-group-item media" v-on:click="onVideoSelect">
    <!-- <img v-bind:src="" /> -->
    <img class="mr-3" :src="thumbnailUrl" />
    <div class="media-body">
      {{ video.snippet.title }}
    </div>
  </li>
</template>

<script>
export default {
  name: 'VideoListItem',
  props: {
    video: Object,
  },
  computed: {
    thumbnailUrl() {
      return this.video.snippet.thumbnails.default.url;
    },
  },
  methods: {
    onVideoSelect() {
      this.$emit('video-select', this.video);
    },
  },
};
</script>

<style scoped>
li {
  display: flex;
  cursor: pointer;
}
li:hover {
  background-color: #eee;
}
</style>
