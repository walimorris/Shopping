<template>
  <div id="app">
    <ShoppingListComponent/>
  </div>
</template>

<script>
import ShoppingListComponent from './components/ShoppingListComponent.vue';

export default {
  name: 'App',
  components: {
    ShoppingListComponent,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
