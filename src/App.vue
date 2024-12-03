<template>
  <div class="app">
    <img alt="Vue logo" src="./assets/poke-logo.png" class="logo-pokemon">
    <h1>¿Quién es ese Pokémon?</h1>
    <PokeList />
  </div>     
</template>

<script>
import PokeList from './components/PokeList.vue';

export default {
  name: 'App',
  components: {
    PokeList
  } 
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  padding: 20px;
  color: #2c3e50;
  margin-bottom: auto;
 
}

.logo-pokemon {
  margin-top: 20px;
  width: 50%;
  height: auto;
}
</style>
