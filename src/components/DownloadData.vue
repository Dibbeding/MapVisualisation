<template>
  <div class="tab" width="100%" object-fit="fill">
    <tr>
      <th class="title">
        Download Data
      </th>
    </tr>
    <tr>
      <th class="normText">
         Here you can download the data with the filters selected in "Filter & Sort" applied.
        
      </th>
    </tr>
    <tr>
      <th class="normText" ref="screen">
        <div v-if="isLoading == 1">
          <button class="button" v-on:click="screenShot()">
            <nobr> Download full data</nobr>
          </button> 
        </div>  
        <div v-else-if="isLoading == 0">   
          <button class="button">
            <nobr> Processing Dowload... </nobr>
          </button> 
        </div>
      </th>
    </tr>
    <tr>
      <th class="normText" ref="screen">
        <div v-if="isLoading == 1">
          <button class="button" v-on:click="screenShot()">
            <nobr> Download filtered data</nobr>
          </button> 
        </div>  
        <div v-else-if="isLoading == 0">   
          <button class="button">
            <nobr> Processing Dowload... </nobr>
          </button> 
        </div>
      </th>
    </tr>


  </div>
</template>

<script>
import html2canvas from 'html2canvas';

export default {
  name: 'DownloadData',
  props: {
    msg: String
  },
  
  data() {
    return {
      isLoading: 1,
    }
  },

  methods: {

    sleep(milliseconds) {
      var start = new Date().getTime();
      for (var i = 0; i < 1e7; i++) {
        if ((new Date().getTime() - start) > milliseconds){
          break;
        }
      }
    },

    screenShot () {
      this.isLoading = 0;

      html2canvas(this.$refs.screen, { backgroundColor: '#FFFFFF', useCORS: true }).then((canvas) => {
        if (navigator.msSaveBlob) { // IE10+ 
          let blob = canvas.msToBlob(); 
          return navigator.msSaveBlob(blob, name); 
        } else {
          let imageurl = canvas.toDataURL('image/png')
          //You need to choose the naming rules yourself
          this.fileDownload(imageurl)
          this.sleep(3000);
          this.isLoading = 1;
        }
      })

    },

    //Download screenshot pictures
    fileDownload(downloadUrl) {
      let aLink = document.createElement("a");
      aLink.style.display = "none";
      aLink.href = downloadUrl;
      aLink.download = `ThisIsTheData.json`;
      // Trigger click-then remove
      document.body.appendChild(aLink);
      aLink.click();
      document.body.removeChild(aLink);
    },


  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.title {
  font-size: xxx-large;
  font-weight: bold;
}

.normText {
  font-weight: normal;
  font-size: large;
}

.tab {
  background-color: rgb(55, 39, 112);
  height: 70vh;
  width: 100%
}


a:link {
  color: rgb(187, 36, 233);
  background-color: transparent;
  text-decoration: none;
}

a:visited {
  color: rgb(252, 74, 133);
  background-color: transparent;
  text-decoration: none;
}

a:hover {
  color: rgb(157, 119, 192);
  background-color: transparent;
  text-decoration: underline;
}

.button {
  outline: none;
  border: none;
  width: 100%;
  height: 18%;
  color: white;
  background-color: rgb(38, 26, 82);
  display:block;
  border-radius: 10px;
  margin-left: auto;
  margin-right: auto;
  margin-top: 10px;
  padding: 10px;


  /* make the text not selectable*/
  -moz-user-select: -moz-none;
  -khtml-user-select: none;
  -webkit-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.button:hover,
.button:focus {
  background-color: rgb(46, 33, 94);
  cursor: pointer;
}

</style>