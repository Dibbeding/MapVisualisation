<template>
  <div class="tab" width="100%" object-fit="fill">
    <table class="helptable">
      <tr>
        <div class="title"> 
          Help 
        </div>
      </tr>
        <tr>
        <div class="normText"> 
          This page contains explanations on the functionalities of the MapTheData program. 
          <br>
          <br>
        </div>
      </tr>


      <tr>
        <div class="smallerTitle"> 
          General Info
        </div>
      </tr>
      <tr>
        <div class="normText"> 
          General Info explanation 
          <br>
          <br>
        </div>
      </tr>


      <tr>
        <div class="smallerTitle"> 
          Glossary
        </div>
      </tr>
      <tr>
        <div class="normText"> 
          Glossary explanation
          <br>
          <br>
        </div>
      </tr>


      <tr>
        <div class="smallerTitle"> 
          Download Data
        </div>
      </tr>
      <tr>
        <div class="normText"> 
          Download Data explanation
          <br>
          <br>
        </div>
      </tr>


      <tr>
        <div class="smallerTitle"> 
          Map
        </div>
      </tr>
      <tr>
        <div class="normText"> 
          Map explanation
          <br>
          <br>
        </div>
      </tr>
    </table>
  </div>
</template>
  

<script>
export default {
  name: 'Help',
  props: {
    msg: String
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
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

.helptable {
  width: 100%;
  /*margin-left: auto;
  margin-right: auto;*/
}

.tab {
  background-color: rgb(55, 39, 112);
  height: 70vh;
  width: 100%;
}

</style>