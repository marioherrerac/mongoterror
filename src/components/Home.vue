<!-- Home.vue -->
<template>
  <div>
    <h2 style="margin-top: 15px">MovieStore Example Site</h2>
      <p>This website offers information on terror movies, directors and producers.</p>
    <ul>
      <li><router-link to='/movie'>Movies information</router-link></li>
      <li><router-link to='/director'>Directors information</router-link></li>
      <li><router-link to='/producer'>Producers information</router-link></li>
    </ul>
  </div>
</template>