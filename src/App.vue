<template>
  <div id="app">
    <upper-tool-bar />
    <table>
      <tr>
        <th>
          <keep-alive>
            <left-tool-bar class="left-toolbar" v-on:change-component="SwitchComponent($event)" />
          </keep-alive>
        </th>
        <th>
          <keep-alive>
            <component v-bind:is="component" averageData="{{ this.averageData }}" v-on:changed-filters="PassAverageData($event)"/>
          </keep-alive>
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
      component:"FilterAndSort",
      averageData:{Country: "Blanc", Value: 0}
  }),
  methods: {
    SwitchComponent(componentType) {
      if (this.component != componentType) {
        this.component = componentType;
      } else {
        this.component = "MapTool"
      }
      return
    },

    PassAverageData(averageData) {
        console.log("Data in de app ", averageData)
        this.averageData = averageData
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