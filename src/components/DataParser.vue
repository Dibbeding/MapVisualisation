<template>

</template>

<script>
import Vue from 'vue'
import VuePapaParse from 'vue-papa-parse'
Vue.use(VuePapaParse)
import { EventBus } from "./event-bus.js";

export default {
  components: {
  },
  props: [],
  data () {
      ""
      null
  },
  mounted () {
      this.parseData;
  },
  created () {
  },
  computed: {
  },
  methods: {
      parseData() {
          this.parsedFile = this.$papa.parse('./DataFiles/liveAnimals.csv')
          console.log(parsedFile)
          EventBus.$emit("transportParsedData", this.parsedFile);
      },
  },

  watch: {
  }
}
</script>

<style scoped lang="scss">

</style>