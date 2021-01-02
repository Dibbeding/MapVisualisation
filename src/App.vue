<template>
  <div id="app">
    <table class="banner">
      <th width="5vw">
      </th>
      <th width="30vw">
        <h1 font-size="small"> <nobr>MapTheData </nobr> </h1>
      </th>
      <th width="5vw">
        <h1>  </h1>
      </th>
      <th width="45vw">
        <h2>
          <nobr> L. Avgen & W. Ebing </nobr>
        </h2>
      </th>
      <th width="300px" align="right" >
        
         <button class="button" v-on:click="SwitchComponent('Help')">
          <!-- Image: Screen Capture by Desainer Kanan from the Noun Project -->
          <img src="./components/Images/QuestionMark.png" alt = "icon" height="40" width="40" align = "center" />
          <br>
          <br> Help
        </button>
        <div class="rightborder" />

      </th>
    </table>

    <table  class="tableCenter">
      <tr>
        <th>
          <keep-alive width="150px" >
            <left-tool-bar class="left-toolbar" v-on:change-component="SwitchComponent($event)" />
          </keep-alive>
        </th>
        <th class="componentplace">
          <keep-alive v-if="checkIfNeedToBeAlive()">
            <component v-bind:is="component" v-bind:getDataset="averageData" v-on:changed-filters="PassAverageData($event)"/>
          </keep-alive>
          <div v-else>
            <component v-bind:is="component" v-bind:getDataset="averageData" v-on:changed-filters="PassAverageData($event)"/>
          </div>
        </th>
        <th>
          <div class="rightborder" />
        </th>
      </tr>
    </table>
  </div>
</template>

<script>
// Tool Bars
import LeftToolBar from './components/LeftToolBar.vue'
// Map
import MapTool from './components/MapTool.vue'
// Side Tools
import FilterAndSort from './components/FilterAndSort.vue'
import GeneralInfo from './components/GeneralInfo.vue'
import Glossary from './components/Glossary.vue'
import DownloadData from './components/DownloadData.vue'
import Help from './components/Help.vue'
import Welcome from './components/Welcome.vue'
import MapWarning from './components/MapWarning.vue'




export default {
  name: 'app',
  components: {
    // Tool Bars
    LeftToolBar,
    // Map
    MapTool,
    // Side Tools
    FilterAndSort,
    GeneralInfo,
    Glossary,
    DownloadData,
    Help,
    Welcome,
  },
  data: () => ({
      component:"Welcome",
      averageData: [],
      value: 30,
  }),

    methods: {
    
    checkIfNeedToBeAlive() {
      if (this.component == "FilterAndSort") return true

      return false
    },

    SwitchComponent(componentType) {
      console.log("Componenttype switch met: ", componentType)
      if (componentType == "MapTool" && this.averageData.length == 0) {
        this.component = MapWarning
        return
      }

      if (this.component != componentType) {
        this.component = componentType;
      }
      return
    },

    PassAverageData(dataPackage) {
        console.log("Data in de app ", dataPackage)
        this.averageData = dataPackage.averageData
        this.component = dataPackage.component
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
  text-align: left;
  color: white;
  margin: 0px;
  background-color:  rgb(25, 17, 54);
  min-height: 100vh;
  min-width: 100vw;
}

.componentplace {
  width: 100%;
  background-color:  rgb(55, 39, 112);
  border-style: solid;
  border-color:  rgb(55, 39, 112);
  border-width: 100px;
  border-radius: 10px;
}

.banner {
  background-color: rgb(25, 17, 54);
  text-align: start;
  color: white;
  font-size: large;
  width: 100vw;
  height: 100px;
  padding-top: 15px;
  padding-bottom: 15px;
  margin-right: auto;
  
  /* make the text not selectable*/
  -moz-user-select: -moz-none;
  -khtml-user-select: none;
  -webkit-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.rightborder {
  width: 10px;
  background-color: rgb(25, 17, 54);
}

.button {
  outline: none;
  border: none;
  height: 80px;
  width: 120px;
  color: white;
  background-color: rgb(25, 17, 54);

}
.button:hover {
  background-color: rgb(37, 25, 80);
  cursor: pointer;
}


</style>
