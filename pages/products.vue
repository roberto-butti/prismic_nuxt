<template>
<div id="products">
  <h1 class="red">{{ name }}!</h1>
      <div class="links">
        <nuxt-link to="/">Index</nuxt-link>
      </div>

</div>
</template>

<script>
export default {
  asyncData (context) {
    var Prismic = require('prismic-javascript')
    var apiEndpoint = process.env.apiPrismicUrl + '/api/v2'
    // var apiToken = '1234567890'
    Prismic.getApi(apiEndpoint /*, {accessToken: apiToken} */).then(function (api) {
      var result = api.query('')
      console.log(result)
      return result // An empty query will return all the documents
    }).then(function (response) {
      console.log('Documents: ', response.results)
    }, function (err) {
      console.log('Something went wrong: ', err)
    })
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