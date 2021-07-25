<template>
  <div>
    <div v-if="$apollo.loading">Loading...</div>
    <br />
    {{ $i18n.locale }}
    <br />
    <nuxt-link v-if="renderComponent" :to="switchLocalePath('en')" @click='local= "en"'>English</nuxt-link>
    <nuxt-link v-if="renderComponent" :to="switchLocalePath('tr_TR')" @click='local= "tr_TR"'>Turkçe</nuxt-link>
    <br />
    <br />
    <br />
    <h1>Hello</h1>
    <Nuxt />
  </div>
</template>
<script>
export default {
  data() {
    return {
      renderComponent: true,
    };
  },
  methods: {
    forceRerender() {
      // Remove my-component from the DOM
      this.renderComponent = false;

      this.$nextTick(() => {
        // Add the component back in
        this.renderComponent = true;
      });
    }
  }
};
</script>
