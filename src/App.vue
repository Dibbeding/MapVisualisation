<template>
  <div id="app">
    <upper-tool-bar />
    <table>
      <tr>
        <th>
          <keep-alive>
            <left-tool-bar v-on:change-component="SwitchComponent($event)" />
          </keep-alive>
        </th>
        <th>
          
            <component v-bind:is="component" />
          
        </th>
      </tr>
    </table>
  </div>
</template>

<script>
// Tool Bars
import LeftToolBar from './components/LeftToolBar.vue'
import UpperToolBar from './components/UpperToolBar.vue'
// Map
import MapTool from './components/MapTool.vue'
// Side Tools
import FilterAndSort from './components/FilterAndSort.vue'
import GeneralInfo from './components/GeneralInfo.vue'
import Glossary from './components/Glossary.vue'
import DownloadData from './components/DownloadData.vue'
import Help from './components/Help.vue'

export default {
  name: 'app',
  components: {
    // Tool Bars
    UpperToolBar,
    LeftToolBar,
    // Map
    MapTool,
    // Side Tools
    FilterAndSort,
    GeneralInfo,
    Glossary,
    DownloadData,
    Help,
  },
  data: () => ({
      component:"MapTool"
  }),
  methods: {
    SwitchComponent(componentType) {
      console.log("Old value = " + this.component)
      if (this.component != componentType) {
        this.component = componentType;
        console.log("New value (1) = " + this.component)
      } else {
        this.component = "MapTool"
        console.log("New value (2) = " + this.component)
      }
      return
    }
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