<!-- BookDetails.vue -->
<template>
  <div class="row">
   <div class="eleven column" style="margin-top: 5%">
    <h2>{{title}}</h2>
     <form>
     <div class="row">
      <div class="six columns">
       <label for="titleInput">Title</label>
       <input class="u-full-width" type="text"
         v-model="movie.title">
      </div>
      <div class="six columns">
       <label for="directorrInput">Director</label>
       <input class="u-full-width" type="text"
          v-model="movie.director">
      </div>
     </div>
     <div class="row">
      <div class="six columns">
       <label for="producerInput">Producer</label>
       <input class="u-full-width" type="text"
          v-model="movie.producer">
      </div>
      <div class="six columns">
       <label for="yearInput">Year</label>
       <input class="u-full-width" type="text"
         v-model="movie.year">
      </div>
     </div>
     <div class="row">
      <div class="six columns">
       <label for="durationInput">Duration</label>
       <input class="u-full-width" type="number"
          v-model="movie.duration">
      </div>
      <div class="six columns">
       <label for="languageInput">Language</label>
       <input class="u-full-width" type="text"
         v-model="movie.language">
      </div>
     </div>
     
     <div class="row">
      <div class="six columns">
       <label for="countryInput">Country</label>
       <input class="u-full-width" type="text"
         v-model="movie.country">
      </div>
     </div>
     <div class="row">
      <router-link class="button button-primary" 
        to="/movie">Back</router-link>
       <a v-if='edit' class="button button-primary" style="float: right"
         v-on:click="updateMovie(movie._id)">Update</a>
       <a v-if='create' class="button button-primary" style="float: right"
         v-on:click="createMovie()">Create</a>
     </div>
    </form>
  </div>
</div>
</template>

<script>
import { useRoute } from 'vue-router'

export default {
  name: "Movie Details",
  props: ['create','edit','create'],
  data() {
    return {
      title: "Movie Data",
      movie: {}
    }
  },
  mounted() {
    const route = useRoute()
    if (route.params.id != null)
      this.findMovie(route.params.id);
    else {
      this.movie = {
        '_id': Math.floor(Math.random()*100000000),'title':'','year':'',
        'duration':0,'language':'','year':0,'country':'','author':'','author_id':0,
        'publisher':'','publisher_id':0 };
    }
  },
  methods: {
    findMovie: function(id) {
      fetch(this.url+'/.netlify/functions/movieFind/'+id,
      { headers: {'Accept': 'application/json'}})
      .then((response) => response.json())
      .then((items) => {
       this.movie = items[0];
      })
    },
    updateMovie: function(id) {
      fetch(this.url+'/.netlify/functions/movieUpdate/'+id,
        { headers: {'Content-Type':'application/json'},
          method: 'PUT',
          body: JSON.stringify(this.movie)})
        .then((data) => {
          this.$router.push('/movie');
        }
      )
    },
    createBMovie: function() {
      fetch(this.url+'/.netlify/functions/movieInsert',
        { headers: {'Content-Type':'application/json'},
          method: 'POST',
          body: JSON.stringify(this.movie)})
        .then((data) => {
           this.$router.push('/movie');
        }
      )
    }
  }
};
</script>