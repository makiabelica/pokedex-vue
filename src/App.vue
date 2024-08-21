<template>
  <div id="app">
    <Pokedex />
  </div>
</template>

<script>
import Pokedex from './components/pokedex.vue';
export default {
  name: 'App',
  components: {
    Pokedex
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: white;
  margin-top: 60px;
}
</style>
