<template>

  <div id="app">
    <sidebar-menu :menu="menu" />
    <div id="club">
      <h1>Rushmere Badminton Club</h1>
    </div>
    <Matches/>
  </div>
</template>

<script>
import Matches from "@/components/Matches";
import 'vue-sidebar-menu/dist/vue-sidebar-menu.css'

export default {
  data() {
    return {
      menu: [
        {
          header: 'Main Navigation',
          hiddenOnCollapse: true
        },
        {
          href: '/',
          title: 'Home',
          icon: 'fa fa-user'
        },
        {
          href: '/matches',
          title: 'Matches',
          icon: 'fa fa-chart-area'
        }
      ]
    }
  },
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
