<template>

  <div id="app">
    <Menu/>
    <div id="club">
      <h1>Rushmere Badminton Club</h1>
    </div>
    <Matches/>
  </div>
</template>

<script>
import Matches from "@/components/Matches";

export default {
  name: 'Rushmere BC',
  components: {
    Matches
  }
}
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
