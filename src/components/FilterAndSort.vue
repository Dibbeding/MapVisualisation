<template>
  <div>
    <h1>Filter & Sort</h1>
    <button v-on:click="ParseData()" class="button">
      Parse
    </button>  
  </div>
</template>

<script>
import VuePapaParse from 'vue-papa-parse'
import Vue from 'vue'
Vue.use(VuePapaParse)

export default {
  name: 'FilterAndSort',
  props: {
    msg: String
  },

  mounted () {
      this.parseData;
  },

  methods: {
      ParseData() {
          let parsedFile = this.$papa.parse('./DataFiles/liveAnimals.csv')
          console.log(parsedFile)
      },
  },
}
</script>

<style scoped>
h1 {
  margin: 40px 0 0;
  background-color: lightpink;
  color:white;
}

</style>