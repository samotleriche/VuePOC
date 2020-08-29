<template>
  <div>
    <SearchBar @termChange="onTermChange"></SearchBar>
    <VideoList></VideoList>
    {{ vidoes.length }}
  </div>
</template>

<script>
import axios from "axios";
import SearchBar from "./components/SearchBar";
import VideoList from "./components/VideoList";
const API_KEY = process.env.VUE_APP_API_KEY;

export default {
  name: "App",
  components: {
    SearchBar: SearchBar,
    VideoList,
  },
  data() {
    return {
      vidoes: [],
    };
  },
  methods: {
    onTermChange(searchTerm) {
      axios
        .get("https://www.googleapis.com/youtube/v3/search", {
          params: {
            key: API_KEY,
            type: "video",
            part: "snippet",
            q: searchTerm,
          },
        })
        .then((res) => {
          this.vidoes = res.data.items;
        });
    },
  },
};
</script>
