<template>
  <table>
    <tr>
      <th>
        <h1 class="banner">Map Visualisation</h1>
      </th>
      <th>
        <h1 class="divider"> || </h1>
      </th>
      <th>
        <h2 class="data-information">
          Hello World
        </h2>
      </th>
      <th>
        <button class="button">
          Help
        </button>
      </th>
    </tr>
  </table>
</template>

<script>
export default {
  name: 'upper-toolbar',
  props: {
  }
}
</script>

<style scoped>
.banner {
  background-color: rgb(38, 26, 82);
  text-align: center;
  vertical-align: center;
  color: white;
  font-size: x-large;
  width: 30vw;
  height: 40px;
  padding-bottom: 5px;
  padding-top: 17px;
  padding-left: 100px;
}

.divider {
  background-color: rgb(38, 26, 82);
  text-align: center;
  vertical-align: center;
  color: white;
  font-size: x-large;
  width: 10vw;
  height: 100%;
  padding-bottom: 5px;
  padding-top: 17px;
  height: 40px;
  /* make the text not selectable*/
  -moz-user-select: -moz-none;
   -khtml-user-select: none;
   -webkit-user-select: none;
   -ms-user-select: none;
   user-select: none;
}

.data-information {
  background-color: rgb(38, 26, 82);
  text-align: center;
  vertical-align: center;
  color: rgb(220, 211, 255);
  font-size: large;
  width: 45vw;
  height: 100%;
  padding-bottom: 0px;
  padding-top: 21.5px;
  height: 40px;
}

.button {
  outline: none;
  border: none;
  min-width: 100px;
  width: 15vw;
  height: 80px;
  padding-bottom: 5px;
  padding-top: 5px;
  color: white;
  background-color: rgb(38, 26, 82);
  display:block;
}
.button:hover,
.button:focus {
  background-color: rgb(55, 39, 112);
}
</style>
