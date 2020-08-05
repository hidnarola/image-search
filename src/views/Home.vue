<template>
  <div class="home">
    <div class="container">
      <h1>Image Search</h1>
      <div class="row mt-5">
        <div class="col">
          <input v-model="searchValue" type="text" class="form-control" />
        </div>
        <div class="col">
          <button class="btn btn-success" @click.prevent="getImages">Search</button>
        </div>
      </div>
      <div class="row mt-5">
        <div class="col my-3" v-for="image in images.hits" :key="image.id">
          <div class="card text-center">
            <div class="card-body">
              <img width="150" height="100" :src="image.previewURL" alt />
            </div>
            <div class="card-footer">
              <span class="material-icons px-2">visibility</span>
              <sup>{{ image.views }}</sup>
              <span class="material-icons px-2">thumb_up_alt</span>
              <sup>{{ image.likes }}</sup>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Home",
  data() {
    return {
      searchValue: "",
      images: []
    };
  },
  methods: {
    getImages() {
      axios
        .get(
          `https://pixabay.com/api/?key=17777732-5881c8153fa2bdcd4d7384430&q=${this.searchValue}&image_type=photo`
        )
        .then(resp => (this.images = resp.data));
    }
  }
};
</script>
