<template>
  <h1 class="red">{{ name }}!</h1>
</template>

<script>
export default {
  asyncData (context) {
    // called every time before loading the component
    return { name: 'Products' }
  },
  fetch () {
    // The fetch method is used to fill the store before rendering the page
  }
  /*,
  head () {
    // Set Meta Tags for this Page
  }
  */
  // and more functionality to discover
}
</script>

<style>
.red {
  color: red;
}
</style>