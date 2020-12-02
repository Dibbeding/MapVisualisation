<template>
  <div class="tab" width="100%" object-fit="fill">
    <tr>
      <th class="title">
        Glossary
      </th>
    </tr>
    <tr>
      <th class="normText">
        Hier komt een heleboel interessante tekst over wat de data inhoudt, mogelijk kan hier ook de legenda aangepast worden.
        
      </th>
    </tr>
  </div>
</template>

<script>
export default {
  name: 'Glossary',
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