<template>
  <div>
    <div>URL: {{ slug }}</div>
    <div v-html="product.name"/>
    <div v-html="product.description"/>
  </div>
</template>

<script>
const PrismicScout = require('prismic-scout');

export default {
  async asyncData ({params}) {
    // called every time before loading the component
    var p ={};
    var Prismic = require("prismic-javascript");
    var apiEndpoint = process.env.apiPrismicUrl + "/api/v2";
    const api = await Prismic.getApi(apiEndpoint /*, {accessToken: apiToken} */)
    const Scout = new PrismicScout(api);
    const { results } = await api.query(
      Prismic.Predicates.at('my.products.uid', params.slug),
      { lang: "en-gb" }
    );

    let product = {};

    if(results.length > 0) {

      product = await Scout.retriveSingle(results, {
        name: {
          _type: 'html'
        },
        description: {
          _type: 'html'
        }
      }).then((p) => p[0]);
    }

    return { slug: params.slug, product }
  },
  head () {
    // Set Meta Tags for this Page
    return {title: 'title'}
  }
}
</script>
