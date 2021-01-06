<template>
  <div class="toolbar">
    <button v-on:click="ChangeComponent(1)" class="button">
      <!-- Image: Filter by Icon Master from the Noun Project -->
      <img src="./Images/Filter.png" alt = "icon" height="70" width="70" align = "center" />
      <br> <br>
      Filter & Sort
    </button>
    <h1 class="whitespace" />
    <button v-on:click="ChangeComponent(2)" class="button">
      <!-- Image: Line Graph by parkjisun from the Noun Project -->
      <img src="./Images/Graph.png" alt = "icon" height="70" width="70" align = "center" />
      <br> <br>
      General Info
    </button>
    <h1 class="whitespace" />
    <button v-on:click="ChangeComponent(3)" class="button">
      <!-- Image: Dictionary by Smalllike from the Noun Project -->
      <img src="./Images/Book.png" alt = "icon" height="70" width="70" align = "center" />
      <br> <br>
      Glossary
    </button>
    <h1 class="whitespace" />
    <button v-on:click="ChangeComponent(4)" class="button">
      <!-- Image: Download by projecthayat from the Noun Project -->
      <img src="./Images/Download.png" alt = "icon" height="70" width="70" align = "center" />
      <br> <br>
      Download Data
    </button>
    <h1 class="whitespace" />
    <button v-on:click="ChangeComponent(5)" class="button">
      <!-- Image: Map by shashank singh from the Noun Project -->
      <img src="./Images/Map.png" alt = "icon" height="100" width="100" align = "center" />
      <br>
      <br> Map
    </button>
  </div>
</template>

<script>
export default {
  name: 'left-toolbar',

  methods: {
    ChangeComponent(id) {
      let component = ""
      switch (id) {
        case 1:
          component = "FilterAndSort"
          break
        case 2:
          component = "GeneralInfo"
          break
        case 3:
          component = "Glossary"
          break
        case 4:
          component = "DownloadData"
          break
        case 5:
          component = "MapTool"
          break
          

      }
      this.$emit('change-component', component)
    }
  }
}
</script>

<style scoped>

.whitespace {
  height: 2.5%;
}

.toolbar {
 width: 150px
}

.button {
  outline: none;
  border: none;
  width: 80%;
  height: 18%;
  color: white;
  background-color: rgb(38, 26, 82);
  display:block;
  border-radius: 10px;
  margin-left: auto;
  margin-right: auto;

  -moz-user-select: -moz-none;
  -khtml-user-select: none;
  -webkit-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.button:hover,
.button:focus {
  background-color: rgb(55, 39, 112);
  cursor: pointer;
}

.toolbar {
  height: 88vh;
  background-color:  rgb(25, 17, 54);
}
</style>