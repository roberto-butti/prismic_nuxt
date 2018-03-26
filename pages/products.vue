<template>
<div id="products">
  <h1 class="red">{{ title }}!</h1>
  <ul>
    <li v-for="value in products">
      <a :href="'/product/'+value.slugs[0]">{{ value.data.nome_prodotto[0].text }}</a>
      
    </li>
  </ul>
  <!-- div>{{ products }}</div  -->
  
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
    return Prismic.getApi(apiEndpoint /*, {accessToken: apiToken} */).then(function (api) {
      var myquery = api.query(
        Prismic.Predicates.at('document.type', 'prodotti'),
        { lang: 'it-it' }
      )
      console.log(myquery)
      return myquery
    }).then(function (response) {
      console.log('Documents: ', response.results)
      return { products: response.results, title: 'Products' }
    }, function (err) {
      console.log('Something went wrong: ', err)
      return { title: err }
    })
    // called every time before loading the component
    // return { products: [], name: 'Products' }
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