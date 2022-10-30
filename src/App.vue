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
import Menu from "@/components/Menu";

export default {
  name: 'Rushmere BC',
  components: {
    Matches,
    Menu
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
