<template>
  <section class="section">
    <div class="is-mobile">

    </div>
  </section>
</template>

<script>
import gql from 'graphql-tag'

export default {
  name: 'HomePage',
  async fetch() {
    const homeresult = await this.$apolloProvider.defaultClient.query({
      query: gql `
          query Query($id: ID!, $locale: [Locale!]!) {
            team(where: {id: $id}, locales: $locale) {
              email
              id
              name
              phone
              slug
              image {
                url
                width
                height
                fileName
              }
              body {
                html
              }
            }
          }`,
      variables() {
        return{
          "id":"ckqmtfgsoxp0x0b088tyo3ytm",
          "locale": ["en"]
        }
      }
    })
    console.log(homeresult)
    this.home = homeresult.data.home
  },
  data () {
    return {
      home: {}
    }
  }
}
</script>
