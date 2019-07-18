<template>
  <div class="container">
    <SearchBar @termChange="onTermChange" />
    <div class="row">
      <VideoDetail :video="selectedVideo" />
      <VideoList :videos="videos" @videoSelect="onVideoSelect" />
    </div>
  </div>
</template>

<script>
import SearchBar from "./components/SearchBar";
import VideoList from "./components/VideoList";
import VideoDetail from "./components/VideoDetail";
import privateKey from "../private-key.json";

export default {
  name: "app",
  data: function() {
    return { videos: [], selectedVideo: null };
  },
  components: {
    SearchBar,
    VideoList,
    VideoDetail
  },
  methods: {
    onTermChange: async function(searchTerm) {
      var url = new URL("https://www.googleapis.com/youtube/v3/search"),
        params = {
          key: privateKey.googleApikey,
          part: "snippet",
          q: searchTerm
        };
      Object.keys(params).forEach(key =>
        url.searchParams.append(key, params[key])
      );
      var response = await fetch(url).then(response => {
        return response.json();
      });

      this.videos = response.items;
      this.selectedVideo = null;
    },
    onVideoSelect: function(video) {
      this.selectedVideo = video;
    }
  }
};
</script>
