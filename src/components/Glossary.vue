<template>
  <div class="tab" width="100%" object-fit="fill">
    <tr>
      <th class="title">
        Glossary
      </th>
    </tr>
    <tr>
      <th class="normText">
        At the moment this function is'nt supported.
        
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