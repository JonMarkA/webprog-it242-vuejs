<template>
  <div class="pun2">
    <h2>{{ name }}</h2>
    <p>{{ message }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: 'Pag inenglish mo yung "tagong sundalo" meron ka na shampoo',
      message: 'Hide n' soldiers'
    }
  }
};
</script>

<style>
 .pun2 {
    border: dashed black 1px;
    display: inline-block;
    margin: 10px;
    padding: 10px;
    background-color: lightgreen;
  }
  #app > div:hover {
  cursor: pointer;
}
</style>