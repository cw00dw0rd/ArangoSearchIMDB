<template>
  <div>
    <div class="">

    <label id="searchLabel" for="searchbox">Movie Title: </label>
    <input id="searchBox" v-model="message" @input="onChange" placeholder="Search..">

    <label id="genreLabel" for="genreSelect">Genre: </label>
    <select id="genreSelect" @change="searchData" v-model="genre">
      <option value="">None</option>
      <hr>
      <option>Action</option>
      <option>Adventure</option>
      <option>Comedy</option>
      <option>Crime</option>
      <option>Drama</option>
      <option>Horror</option>
      <option>Suspense</option>
    </select>
  </div>
<div class="row">

      <ul v-show="isOpen" class="autocomplete-results" style="list-style: none;">
        <li v-for="(result, i) in info" :key="i" class="autocomplete-result">
          <div class="column">
          <div class="card">
          <h1>{{ result.title }}</h1>
          <h2>Description: </h2><p>{{ result.description}}</p>
          <p>Genre: {{ result.genre }}</p>
          <div v-if="result.studio">
            <p>Studio: {{result.studio}}</p>
          </div>
          <div v-if="result.trailer">
            <a v-bind:href="result.trailer">Watch Trailer</a>
          </div>
          <div v-else>
            <p>No trailer supplied</p>
          </div>
        </div>
      </div>
        </li>
      </ul>
    </div>
  </div>

</template>
<script>
import axios from 'axios'

export default {
  name: 'Search',
  props: {
    msg: String
  },
  data: function() {
    return {
      info: 0,
      message: '',
      genre: '',
      results: '',
      isOpen: false,
      selected: '',
      trailerLink: ''
      }
},
methods: {
  onChange() {
    this.searchData();
    this.message.length > 0 ? this.isOpen = true : this.isOpen = false;
  },
  searchData () {
    axios
    .post("http://127.0.0.1:8529/_db/imdb/search/titlesearch", {"type": "Movie", "label": this.message, "genre": this.genre})
    .then(response => {
      this.info = response.data
    })
  }
}
}
</script>
<style scoped>
#searchLabel {
  font-weight: bold;
}
#searchBox {
  margin-right: 20px;;
  margin-left: 5px;
}
#genreLabel {
  font-weight: bold;
}
#genreSelect {
  margin-left: 5px;
}

.row {
  margin: auto;
  width: 75vw;
}
/* Float four columns side by side */
.column {
  float: left;
  padding: 20px;
}
.column h1 {
  font-size: 20px;
}
.column h2 {
  font-size: 18px;
}
.column p {
  font-size: 16px;
}
.column a {
  font-size: 16px;
}
.card {
  height: 42vh;
  width: 40vh;
  margin: auto;
}
/* Clear floats after the columns */
.row:after {
  content: "";
  display: table;
  clear: both;
}

/* Responsive columns */
@media screen and (max-width: 600px) {
  .column {
    width: 100%;
    display: block;
    margin-bottom: 20px;
  }
}

/* Style the counter cards */
.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  padding: 16px;
  text-align: center;
  background-color: #f1f1f1;
}
</style>
