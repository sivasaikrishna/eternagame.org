<template>
  <div id="app">
    <Navbar />
    <VueBootstrapBreakpointIndicator style="z-index: 1070" />
    <Modals />
    <router-view />
  </div>
</template>
<script lang="ts">
  import { Component, Prop, Vue } from 'vue-property-decorator';
  import VueBootstrapBreakpointIndicator from 'vue-bootstrap-breakpoint-indicator/src/BootstrapBreakpointIndicator.vue';
  import Navbar from '@/components/PageLayout/Navbar/Navbar.vue';
  import Modals from '@/components/Modals/Modals.vue';
  import i18n, { LANGUAGES, DEFAULT_LANGUAGE, LANGUAGE_COOKIE_NAME } from '@/plugins/i18n';
  // @ts-ignore
  import browserLanguage from 'in-browser-language';
  // @ts-ignore
  import Cookies from 'js-cookie';

  import Vuetify from 'vuetify';
  // @ts-ignore
  import { TiptapVuetifyPlugin } from 'tiptap-vuetify';

  // Vuetify Object (as described in the Vuetify 2 documentation)
  const vuetify = new Vuetify();

  // use Vuetify's plugin
  Vue.use(Vuetify);
  // use this package's plugin
  Vue.use(TiptapVuetifyPlugin, {
    // the next line is important! You need to provide the Vuetify Object to this place.
    vuetify, // same as "vuetify: vuetify"
    // optional, default to 'md' (default vuetify icons before v2.0.0)
    iconsGroup: 'md',
  });

  if (
    process.env.VUE_APP_ENV === 'client'
    && window.navigator.cookieEnabled
    && !Cookies.get(LANGUAGE_COOKIE_NAME)
  ) {
    Cookies.set(LANGUAGE_COOKIE_NAME, browserLanguage.pick(LANGUAGES));
    window.location.reload();
  }

  @Component({
    components: {
      Navbar,
      VueBootstrapBreakpointIndicator,
      Modals,
    },
  })
  export default class App extends Vue {}
</script>

<style lang="scss">
  @import '@/styles/global.scss';

  // Import Bootstrap and BootstrapVue source SCSS files
  @import '~bootstrap/scss/bootstrap.scss';
  @import '~bootstrap-vue/src/index.scss';

  @import '@/styles/_bootswatch.scss';
  @import '@/styles/custom.scss';
</style>
