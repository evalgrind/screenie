<script>
import axios from 'axios';

export default {
  name: 'App',

  data() {
    return {
      websiteUrl: '',
      thumbnailUrl: ''
    }
  },

  methods: {
    makeWebsiteThumbnail() {
      // Call the Go API, in this case we only need the URL parameter.
      axios.post("http://localhost:3000/api/thumbnail", {
        url: this.websiteUrl,
      })
        .then((response) => {
          this.thumbnailUrl = response.data.screenshot;
        })
        .catch((error) => {
          window.alert(`The API returned an error: ${error}`);
        })
    }
  }
}
</script>

<template>
  <div id="app" class="container">
    <div class="row">
      <div class="col-md-6 offset-md-3 py-5">
        <h1>Screenies</h1>
        <p>Create thumbnails for a website.</p>

        <form v-on:submit.prevent="makeWebsiteThumbnail">
          <div class="form-group">
            <input v-model="websiteUrl" type="text" id="website-input" placeholder="Website URL" class="form-control">
          </div>
          <div class="form-group">
            <button class="btn btn-primary">Generate!</button>
          </div>
        </form>
        <img :src="thumbnailUrl" />
      </div>
    </div>
  </div>
</template>