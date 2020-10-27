<template>
  <div id="app" class="small-container">
    <upper-tool-bar />
    <table>
      <tr>
        <th>
          <left-tool-bar />
        </th>
        <th>
          <map-tool />
        </th>
      </tr>
    </table>
  </div>
</template>

<script>
//https://www.w3schools.com/howto/tryit.asp?filename=tryhow_js_overlay
//https://codesandbox.io/s/vuejssidebarmenuburgerobservable-iv1zc?file=/src/components/Menu/Sidebar.vue
import LeftToolBar from './components/LeftToolBar.vue'
import UpperToolBar from './components/UpperToolBar.vue'
import MapTool from './components/MapTool.vue'

export default {
  name: 'App',
  components: {
    LeftToolBar,
    UpperToolBar,
    MapTool,
  }
}
</script>

<style>

 * {
       margin: 0;
   }

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  margin: 0px;
  background-color: rgb(38, 26, 82);
  min-height: 100vh;
  min-width: 100vh;
}

</style>
