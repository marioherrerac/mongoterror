<!-- BookIndex.vue -->
<template>
  <div class="row">
   <div style="margin-top: 5%">
     <h2>{{title}}</h2>
     <table><thead>
       <tr>
         <th>Title</th>
        <th>Director</th>
        <th>Producer</th>
        <th>Year</th>
        <th class="text-center">Actions</th>
	   </tr>
       </thead><tbody>
       <tr v-for='movie in movies' :key="movie.id">
       <td>{{movie.title}}</td>
       <td>{{movie.director}}</td>
       <td>{{movie.producer}}</td>
       <td>{{movie.year}}</td>
       <td>
       <router-link class="button"
         :to="'/movie/show/'+book._id">Show</router-link>
       &nbsp;
       <router-link class="button"
         :to="'/movie/edit/'+book._id">Edit</router-link>
       &nbsp;
       <a class="button"
         v-on:click="deleteMovie(movie._id)">Erase</a>
       </td>
       </tr></tbody>
     </table>
     <router-link class="button button-primary" 
       to="/movie/create">New</router-link>
   </div>
  </div>
</template>

<script>
	
export default {
  name: "Movie Index",
  data() {
    return {
      title: 'Movie List',
      movies: []
    };
  },
  mounted() {
    this.allMovies()
  },
  methods: {
    allMovies() {
      fetch(this.url+'/.netlify/functions/movieFindAll',
        { headers: {'Accept': 'application/json'}})
        .then((response) => response.json())
        .then((items) => {
          this.movies = items;
        })
     },
     deleteMovie(id) {
       fetch(this.url+'/.netlify/functions/movieDelete/'+id,
         { headers: {'Content-Type': 'application/json'},
           method: 'DELETE'})
          .then((items) => {
            this.allMovies();
          }
        )
     }
  }
};
</script>