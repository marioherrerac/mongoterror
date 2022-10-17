<template>
  <div id="app" class="container">
    <div class="row"  style="margin-top: 15px">
      <router-link class="three columns button button-primary" 
        to="/">Home</router-link>
      <router-link class="three columns button button-primary" 
        to="/movie">Movies</router-link>
      <router-link class="three columns button button-primary" 
        to="/director">Directors</router-link>
      <router-link class="three columns button button-primary" 
        to="/producer">Producers</router-link>
    </div>
   <router-view />
    <div class="row">
      <button disabled="disabled" class="twelve columns button-primary">
        Copyright (c) 2020 - Armando Arce-Orozco
      </button>
    </div>
  </div>
  </template>
  
  <script>
  export default {
    name: "App",
  };
  </script>