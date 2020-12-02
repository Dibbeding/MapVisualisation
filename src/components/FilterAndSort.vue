<template>
  <div class="tab" width="100%" object-fit="fill">
    <table class="filtertable">
      <tr>
        <th class="title">
          Filter & Sort 
        </th>
      </tr>
      <tr>
        <th class="normText">
          Select which data you would like to see by selecting a subject in the form below. <br> {{" "}} <br>
        </th>
      </tr>
      <tr class="listspot">
        <div class="input-group">
          <select v-model="selectedItemSet" single class="subjectlist">
            <option v-for="dataset in datasetList" v-bind:key="dataset.name">
              {{dataset.name}}
            </option>
          </select>
          <button v-on:click="datasetSelected()" class="filterbuttons">
            Confirm
          </button> 
        </div>
      </tr>

      <tr>
        <th class="normText">
          Select which subsection of the data you would like to see by selecting it in the form below. <br> {{" "}} <br>

        </th>
      </tr>
      <tr class="listspot">
        <div class="input-group">
          <select v-model="selectedItem" single class="subjectlist">
            <option v-for="subject in datasetList[selectedItemIndex].subjects" v-bind:key="subject">
              {{subject}}
            </option>
          </select>
          <button v-on:click="computeAverage()" class="filterbuttons">
            Confirm
          </button> 
        </div>
      </tr>

      <tr>
        <th class="smallerTitle">
          <br>
          More information
        </th>
      </tr>
      <tr>
        <th class="normText">
          Clarifications on how to read the data can be found in the "Glossary"-tab. <br>
          <br>
          General information about the used datasets can be found in the "General Info"-tab
        </th>
      </tr>
    </table>
    <!-- 
    <button v-on:click="ParseData()" class="button">
      Parse
    </button> 
    <button v-on:click="SelectYears()" class="button">
      Years
    </button> 
    
    <button v-on:click="applyFilters()" class="button">
      Apply
    </button>  -->
  </div>
</template>

<script>
import ChickenData from './DataFiles/chickenData.json'
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
      selectedItem: "",
      selectedItemSet: "",
      selectedItemIndex: 0, // TODO, -1 als begin

      datasetList: [
        { name: "Live Animals", subjects: ["Chickens","Dogs","Cats"] },
        { name: "Live Stock", subjects: ["Chickens","Cows","Pigs"] },
        { name: "Filler", subjects: ["Filler1","Filler2","Filler3"] }
        ],
    }
  },

  created : function() {
      // Turn the JSON into better structered data
      this.parseData;
      let DataSet = ChickenData
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
    this.selectedItem;
  },

  methods: {

    datasetSelected() {
      for (let i = 0; i < this.datasetList.length; i++) {
        if (this.selectedItemSet == this.datasetList[i].name) {
          this.selectedItemIndex = i; 
        }
      }

      console.log(this.datasetList[this.selectedItemIndex].subjects)
    },

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
      // First select which dataset to use:
      if (this.selectedItem == "Chickens") {
          // TODO
      } else {
        return;
      }


      this.curYearRange = { lowYear: 1990, highYear: 1995 }
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
      console.log("Basisjaar: ", largestIndex + this.indexSub)
      // Use this array to know the divider for the average calculation
      let averageDivider = new Array(averageData.length)
      for (var i = 0; i < averageData.length; i++) { averageDivider[i] = 1 }

      // First calculate the total
      // Iterate over all years
      for (let indexYear = this.curYearRange.lowYear; 
           indexYear <= this.curYearRange.highYear; indexYear++) {
        console.log("Dit jaar: ", indexYear)
        // Iterate over all countries if the year is not used for the basis
        if (indexYear != (largestIndex + this.indexSub)) {
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
                  //console.log("SKIP LAND")
                  //if (indexCountry < 10) { console.log("Country not yet found: ", countryB) }
                  --offsetIndex
                  continue;
      
                // Country A == Country B, their values can be added
                case 0:
                  //console.log("SAME LAND")
                  if (countryA == "Netherlands") { console.log("Before adding: ", averageData[indexCountry]) }
                  averageData[indexCountry].Value += this.fullData[indexYear - this.indexSub].Year[indexCountry + offsetIndex].Value
                  averageDivider[indexCountry]++
                  if (countryA == "Netherlands") { console.log("After adding: ", averageData[indexCountry]) }
                  break;

                // Country B needs to be inserted into the list
                case 1:
                  /*console.log(" \n \nCountry original = ", countryA)
                  console.log("thing to insert = ", countryB)
                  console.log("Result: ", result)
                  console.log("indexCountry: ", indexCountry)
                  console.log("Offset: ", indexCountry + offsetIndex)
                  console.log("INSERT LAND")*/
                  //console.log("country")
                  averageData.splice(indexCountry, 0, cloneDeep(this.fullData[indexYear - this.indexSub].Year[indexCountry + offsetIndex]))
                  averageDivider.splice(indexCountry, 0, 1) 
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
      //console.log("Average: ", averageData)
      this.$emit('changed-filters', averageData);
      console.log(this.selectedItem)
    },

    applyFilters() {
      
    },
  },
}
</script>

<style scoped>

.title {
  font-size: xxx-large;
  font-weight: bold;
}

.smallerTitle {
  font-size: xx-large;
  font-weight: bold;
}

.normText {
  font-weight: normal;
  font-size: large;
}

.tab {
  background-color: rgb(55, 39, 112);
  height: 70vh;
  width: 100%;
}

.buttonspot {
  height: 50px;
  width: auto;
}

.filterbuttons {
  height: 25px;
  width: 100px;
  display: inline-block;
  margin-left: 10px;
  
}

.filterbuttons:hover {
  cursor: pointer;
}

.filtertable {
  width: 100%;
  /*margin-left: auto;
  margin-right: auto;*/
}

.subjectlist {
  width: 200px;
  scale: 1;
}

.listspot {
  height: 50px;
  width: 100%;
}

</style>