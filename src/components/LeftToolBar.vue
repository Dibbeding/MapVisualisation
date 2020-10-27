<template>
  <div>
    <button class="button">
      Filter & Sort
    </button>
    <button class="button">
      General Info
    </button>
    <button class="button">
      Glossary
    </button>
    <button class="button">
      Download Data
    </button>
    <button class="button">
      Screen Capture
    </button>
  </div>
</template>

<script>
export default {
  name: 'left-toolbar',
}
</script>

<style scoped>


.button {
  outline: none;
  border: none;
  min-width: 100px;
  width: 5vw;
  height: 19.2vh;
  color: white;
  background-color: rgb(38, 26, 82);
  display:block;
}
.button:hover,
.button:focus {
  background-color: rgb(55, 39, 112);
}
</style>