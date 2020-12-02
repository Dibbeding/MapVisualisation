<template>
  <div class="tab" width="100%" object-fit="fill">
    <tr>
      <th class="title">
        Welcome
      </th>
    </tr>
    <tr>
      <th class="normText">
        This application has been developed by Lal Avgen and Wouter Ebing for <br> 
        the course "Human Computer Interaction & Information Visualisation". <br>
        <br>
        The goal of the application is to improve aspects of map-based visualisations of global data. <br>
        The data used originates from edited versions of datasets from the <a href="http://www.fao.org/faostat/en/#home" font-color="white">Food and Agriculture <br>
        Organization (FAO)</a>. <br>
        <br>
        In order to get started, open the "Filter & Sort"-tab by clicking the button on the left. <br>
        There you can select a subject, which will be visualized in the "Map"-tab. For more information <br>
        about the datasets, you can click the button for the "Glossary"-tab. If you want to save the current <br>
        visualisation, you can click the "Screen Capture"-button on the top-right while on the "Map"-tab. <br>
        <br>
        If something seems unclear, you can press the "Help"-button on the top-right. This will direct you <br>
        to a page with instructions.
        
      </th>
    </tr>
  </div>
</template>

<script>
export default {
  name: 'Welcome',
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



</style>