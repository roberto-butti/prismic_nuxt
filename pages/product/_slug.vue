<template>
  <div>
    Prodotto: {{ slug }}
  </div>
</template>

<script>
export default {
  asyncData (context) {
    // called every time before loading the component
    console.log(context.params.slug)
    return { slug: context.params.slug }
    // return {}
  },
  head () {
    // Set Meta Tags for this Page
    return {title: 'titolo'}
  }
}
</script>
