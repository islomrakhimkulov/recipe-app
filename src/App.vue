<template>
  <div class="container">
    <recipe-app />
  </div>
</template>

<script>
import RecipeApp from './components/RecipeApp';

export default {
  name: 'App',
  components: {
    RecipeApp
  }
}
</script>

<style>
body{
    background-image: linear-gradient( 65.4deg,  rgba(56,248,249,1) -9.1%, 
    rgba(213,141,240,1) 48%, rgba(249,56,152,1) 111.1% );
}
</style>

// day one 28.11.2021 
