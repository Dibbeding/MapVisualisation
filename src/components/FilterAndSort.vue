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
    <button v-on:click="applyFilters()" class="button">
      Apply
    </button> 
  </div>
</template>

<script>
import DataSet from './DataFiles/chickenData.json'
import { cloneDeep } from "lodash" // To create actual copies of objects
//https://www.convertcsv.com/csv-to-json.htm

export default {
  name: 'FilterAndSort',
  data() {
    return {
      fullData: [],
      partialData: [],
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
      //console.log("Check fullData in created: ", this.fullData)
  },

  mounted () {
    this.fullData;
    this.partialData;
    this.indexSub;   
    this.yearRange;
    this.curYearRange;
  },

  methods: {

    ParseData() {
      //console.log("fullData: ", this.fullData)
      //let temp = this.fullData[2018 - this.indexSub]
      //console.log(temp)
      //console.log(this.fullData[2018 - this.indexSub].Year[0])
    },

    SelectYears() { 
      // Empty if not empty
      while (this.partialData.length > 0) { this.partialData.pop() }
      
      // Only put needed years in this object
      this.curYearRange = { lowYear: 1961, highYear: 1962 } // TODO make selectable
      for (let index = this.curYearRange.lowYear; index <= this.curYearRange.highYear; index++) {
        this.partialData.push(this.fullData[index - this.indexSub])
      }
      //console.log("filtered partial: ", this.partialData)
      //console.log("filtered fullData: ", this.fullData)
    },

    computeAverage() {


      this.curYearRange = { lowYear: 1961, highYear: 1962 }
      //console.log("Check fullData in computeAverage: ", this.fullData)

      // Find the year with the most countries to use as a basis
      let largestLength = 0, largestIndex = -1;
      for (let indexYear = (this.curYearRange.lowYear - this.indexSub); 
           indexYear <= this.curYearRange.highYear - this.indexSub; indexYear++) {

        if (this.fullData[indexYear].Year.length > largestLength) {
          largestLength = this.fullData[indexYear].Year.length
          largestIndex = indexYear
        }

      }
      let averageData = cloneDeep(this.fullData[largestIndex].Year)

      // Use this array to know the divider for the average calculation
      let averageDivider = new Array(averageData.length)
      for (var i = 0; i < averageData.length; i++) { averageDivider[i] = 1 }

      // First calculate the total
      // Iterate over all years
      for (let indexYear = (this.curYearRange.lowYear + 1); 
           indexYear <= this.curYearRange.highYear; indexYear++) {

        // Iterate over all countries if the year is not used for the basis
        if (indexYear != largestIndex) {

          let offsetIndex = 0
          for (let indexCountry = 0; indexCountry < averageData.length; indexCountry++) {

            // If the value is not null, check if it can be added
            if (this.fullData[indexYear - this.indexSub].Year[indexCountry + offsetIndex].Value != null) { 

              // Check if the country is the same, already in the list, or needs to be added
              let countryA = averageData[indexCountry].Country
              let countryB = this.fullData[indexYear - this.indexSub].Year[indexCountry + offsetIndex].Country
              let result = countryA.localeCompare(countryB)

              switch (result) {
                // CountryB might be found later
                case -1:
                  //if (indexCountry < 10) { console.log("Country not yet found: ", countryB) }
                  --offsetIndex
                  continue;
      
                // Country A == Country B, their values can be added
                case 0:
                  //if (indexCountry < 10) { console.log("Before adding: ", averageData) }
                  averageData[indexCountry].Value += this.fullData[indexYear - this.indexSub].Year[indexCountry + offsetIndex].Value
                  averageDivider[indexCountry]++
                  //if (indexCountry < 10) { console.log("After adding: ", averageData) }
                  break;

                // Country B needs to be inserted into the list
                case 1:
                  //console.log("Index to insert = ", indexYear)
                  //console.log("thing to insert = ", this.fullData[indexYear - this.indexSub].Year[indexCountry + offsetIndex])
                  averageData.splice((indexYear - this.indexSub), 0, cloneDeep(this.fullData[indexYear - this.indexSub].Year[indexCountry + offsetIndex]))
                  averageDivider.splice((indexYear - this.indexSub), 0, 1)
                  //console.log("Average after: ", averageData)
                  break;
              }//switch
            }//if
          }//for
        }//if
      }//for

      // Secondly calculate the average !!! Shit ik moet ook rekening houden met null values
      for (let indexCountry = 0; indexCountry < averageData.length; indexCountry++) {
        //console.log("Value ", averageData[indexCountry].Value)
        //console.log("Divider: ",  averageDivider[indexCountry])
        averageData[indexCountry].Value /= averageDivider[indexCountry]
      }
      console.log("Average: ", averageData)
      this.$emit('changed-filters', averageData);
    },

    applyFilters() {
      
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