<template>
  <div class="tab" width="100%" object-fit="fill">
    <tr>
      <th class="title">
        General Information
      </th>
    </tr>
    <tr>
      <th class="normText">
         Hier gaan we uitleggen waar de data vandaan komt, maar ook hoe het verzamelt is (?), ik denk dat het ook handig is om
         op deze plek de "waarschuwing" te zetten over beslissingen van landen. Misschien ook dat enkele namen aangepast zijn?
        
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