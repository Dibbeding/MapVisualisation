<template>
  <div class="tab">
    <div class="title"> Filter & Sort </div>
    <button v-on:click="ParseData()" class="button">
      Parse
    </button> 
    <button v-on:click="SelectYears()" class="button">
      Years
    </button> 
    <button v-on:click="computeAverage()" class="button">
      Average
    </button> 
  </div>
</template>

<script>
import DataSet from './DataFiles/chickenData.json'
//https://www.convertcsv.com/csv-to-json.htm

export default {
  name: 'FilterAndSort',
  data() {
    return {
      fullData: [],
      partialData: [],
      averageData: [],
      indexSub: 0,
      yearRange: 0,
      curYearRange: 0,
    }
  },

  created : function() {
      // Turn the JSON into better structered data
      this.parseData;
      let oldYear = DataSet[0]["Year"], year;
      let yearData = new Array();

      // First calculate indexSub
      this.indexSub = DataSet[0]["Year"]

      for (let index = 0; index < DataSet.length; index++) {
        year = DataSet[index]["Year"]

        // If a new year is found, add all the countries of the previous year to fullData
        if (oldYear != year) {
          this.fullData.push({Year: yearData})
          yearData = new Array();
          oldYear = year
        }

        let countryName = DataSet[index]["Country"]
        let value = DataSet[index]["Value"]        
        yearData.push({Country: countryName, Value: value})
      }

      // Add last year to fullData
      this.fullData.push({Year: yearData})

      // Set year range for selecting
      this.yearRange = { lowestYear: this.indexSub, highestYear: (this.indexSub + this.fullData.length) }
  },

  mounted () {
    this.fullData;
    this.partialData;
    this.averageData;
    this.indexSub;   
    this.yearRange;
    this.curYearRange;
  },

  methods: {

    ParseData() {
      console.log("fullData: ", this.fullData)
      //let temp = this.fullData[2018 - this.indexSub]
      //console.log(temp)
      //console.log(this.fullData[2018 - this.indexSub].Year[0])
    },

    SelectYears() { 
      // !!! partialData needs to be set before calling
      // Empty if not empty
      while (this.partialData.length > 0) { this.partialData.pop() }
      
      // Only put needed years in this object
      this.curYearRange = { lowYear: 1961, highYear: 1962 } // TODO make selectable
      for (let index = this.curYearRange.lowYear; index <= this.curYearRange.highYear; index++) {
        this.partialData.push(this.fullData[index - this.indexSub])
      }
      console.log("filtered: ", this.partialData)
    },

    computeAverage() {

      // Put the first year as a basis
      this.averageData = this.fullData[this.curYearRange.lowYear - this.indexSub]

      // First calculate the total
      // Iterate over all years
      for (let indexYear = (this.curYearRange.lowYear + 1); indexYear <= this.curYearRange.highYear; indexYear++) {
        // Iterate over all countries
        for (let indexCountry = 0; indexCountry < this.averageData.Year.length; indexCountry++) {
          this.averageData.Year[indexCountry].Value += this.fullData[indexYear - this.indexSub].Year[indexCountry].Value
        }
      }
      console.log("Average: ", this.averageData)

      // Secondly calculate the average
      let divider = (this.curYearRange.highYear - this.curYearRange.lowYear ) + 1;
      for (let indexCountry = 0; indexCountry < this.averageData.Year.length; indexCountry++) {
        this.averageData.Year[indexCountry].Value /= divider
      }

      console.log("Average: ", this.averageData)

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

.title {
  position: center;
  font-size: x-large;
}

.tab {
  background-color: rgb(109, 85, 194);
  height: 100%;
  widows: 100%;
}

</style>