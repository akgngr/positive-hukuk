<!-- Please remove this file from your project -->
<template>
  <div>
    <div v-if="$apollo.loading">Loading...</div>
    <h1>Services</h1>
    <br />
    {{ $i18n.locale }}
    <br />
    <a
      href="#"
      v-for="locale in availableLocales"
      :key="locale.code"
      @click.prevent.stop="$i18n.setLocale(locale.code)">{{ locale.name }}</a>
    <br />
    <nuxt-link
      v-for="locale in availableLocales"
      :key="locale.code"
      :to="switchLocalePath(locale.code)">{{ locale.name }}</nuxt-link>
    <br />
    <nuxt-link to="/en">English</nuxt-link>
    <nuxt-link :to="switchLocalePath('tr_TR')">Turkçe</nuxt-link>
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
  computed: {
    availableLocales () {
      return this.$i18n.locales.filter(i => i.code !== this.$i18n.locale)
    }
  },
  methods: {
    switchLocale(locale) {
      if (this.$i18n.locale !== locale) {
        this.$i18n.locale = locale
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
            "servicesLocales": [this.$i18n.locale] || ["tr_TR"]
          }
        },
        data: locales => [this.$i18n.locale]
      }
    }
  }
}
</script>
