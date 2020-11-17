<template>
  <div>
    <button v-on:click="ChangeComponent(1)" class="button">
      Filter & Sort
    </button>
    <button v-on:click="ChangeComponent(2)" class="button">
      General Info
    </button>
    <button v-on:click="ChangeComponent(3)" class="button">
      Glossary
    </button>
    <button v-on:click="ChangeComponent(4)" class="button">
      Download Data
    </button>
    <button v-on:click="ChangeComponent(5)" class="button">
      Help
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
          break;
        case 2:
          component = "GeneralInfo"
          break;
        case 3:
          component = "Glossary"
          break;
        case 4:
          component = "DownloadData"
          break;
        case 5:
          component = "MapTool"
          break;
          

      }
      this.$emit('change-component', component);
    }
  }
}
</script>

<style scoped>


.button {
  outline: none;
  border: none;
  min-width: 100px;
  width: 5vw;
  height: 19.2vh;
  color: white;
  background-color: rgb(38, 26, 82);
  display:block;
}
.button:hover,
.button:focus {
  background-color: rgb(55, 39, 112);
}
</style>