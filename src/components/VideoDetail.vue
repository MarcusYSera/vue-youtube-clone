<template>
  <div v-if="video" class="col-md-8">
    <div class="details">
      <div class="embed-responsive embed-responsive-16by9">
        <iframe class="embed-responsive-item" v-bind:src="videoURL" />
      </div>
      <h4>
        {{ displayVideoTitle }}
      </h4>
      <p>
        {{ video.snippet.description }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'VideoDetail',
  props: {
    video: Object,
  },
  computed: {
    displayVideoTitle() {
      return this.video.snippet.title;
    },
    videoURL() {
      const { videoId } = this.video.id;
      return `https://www.youtube.com/embed/${videoId}`;
    },
  },
};
</script>

<style scoped>
.details {
  margin-top: 10px;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 4px;
  background-image: linear-gradient(to right, #29323c, #485563);
}
</style>
