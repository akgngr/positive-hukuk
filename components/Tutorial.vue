<!-- Please remove this file from your project -->
<template>
  <div>
    <ul>
      <li v-for="service in services" :key="service.id" class="pb-4 b-border">
        <h2>{{service.name}}</h2>
        <p>{{service.slug}}</p>
        <p v-html="service.body.html"></p>
      </li>
    </ul>

  </div>
</template>

<script>
import gql from 'graphql-tag'

export default {
  data() {
    return{
      local: this.$i18n.locale,
    }
  },
  methods: {
    switchLocale() {
      if (this.$i18n.locale === "tr_TR") {
        return{
          local: "tr_TR"
        }
      } else{
        return{
          local: "en"
        }
      }
    }
  },
  apollo: {
    services() {
      return{
        query: gql`
        query getServices($servicesLocales: [Locale!]!) {
          services(locales: $servicesLocales) {
            id
            name
            slug
            body {
              html
            }
          }
        }
      `,
        variables() {
          return{
            "servicesLocales": [this.local]
          }
        }
      }
    }
  }
}
</script>
