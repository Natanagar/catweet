<template>
  <div  id="app">
    <CatProfile/>
  </div>
</template>

<script>
  import CatProfile from "./components/CatProfile";

export default {
  name: 'App',
  components : { CatProfile },
  data(){
    return{};
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  display : flex;
  flex-direction: column;
}

</style>
