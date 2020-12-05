<template>
  <div class="tab" width="100%" object-fit="fill">
    <tr>
      <th class="title">
        General Information
      </th>
    </tr>
    <tr>
      <th class="smallerTitle">
        This application
      </th>
    </tr>
    <tr>
      <th class="normText">
        This application has been created for a research project of the course <br>
        "Human Computer Interaction and Information Visualisation". The aim of this <br>
        application is to show the potentisal of an improved visualisation for global data. <br>
        The datasets used within this program come from the <a href="http://www.fao.org/faostat/en/#home" font-color="white">Food and Agriculture <br>
        Organization (FAO)</a>. The map was made using leaflet and a geoJSON-file of the eart <br>
        from  <a href="https://geojson-maps.ash.ms/" font-color="white">this website</a>.
        <br>
        <br>
      </th>
    </tr>
    <tr>
      <th class="smallerTitle">
        FAOSTAT-data
      </th>
    </tr>
    <tr>
      <th class="normText">
        As mentioned above, the datasets used originate from the FAOSTAT-organisation. <br>
        Certain edits had to be made to the datasets, which are the following:
        <ul>
          <li>Only columns containing the country name, value and year have been kept </li>
          <li>Certain country names have been replaced by their geoJSON counterpart, for <br>
              the sake of briefity </li>
          <li>Countries that have no counterpart in the geoJSON-file (e.g. due to not <br>
              existing anymore), can not be represented in the map </li>
         </ul>
        <br>
        <br>
      </th>
    </tr>
    <tr>
      <th class="smallerTitle">
        GeoJSON-data
      </th>
    </tr>
    <tr>
      <th class="normText">
        The geoJSON-file used by the leaflet map is in the public domain. It only includes countries <br>
        that currently exist.
        <br>
        <br>
      </th>
    </tr>
    <tr>
      <th class="smallerTitle">
        Disclaimer
      </th>
    </tr>
    <tr>
      <th class="normText">
        FAOSTAT does not recognize certain geographical locations as their own countries. This is <br>
        the case for:
        <ul>
          <li>North Cyprus </li>
          <li>Somaliland </li>
          <li>Taiwan </li>
         </ul>
         Due to the lack of data in the used datasets, these countries don't have their seperate data <br>
         within this program. The decision to use data that does not recognize these countries is due to <br>
         the comparison we could make against their own visualisation. Not including these countries is <br>
         not a reflection of your personal opinions.

        <br>
        <br>
      </th>
    </tr>
  </div>
</template>

<script>
export default {
  name: 'GeneralInfo',
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