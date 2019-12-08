<template>
  <v-app dark>
    <v-app-bar fixed app>
      <v-toolbar-items>
        <v-btn text
          href="https://qiita.com/advent-calendar/2019/nuxt-js"
          target="_blank"
          rel="noopener noreferrer"
        >
          <logo />
          <v-toolbar-title class="text-capitalize" v-text="title"/>
        </v-btn>
      </v-toolbar-items>

      <v-spacer></v-spacer>

      <v-toolbar-items>
        <v-btn text
          href="https://vuetifyjs.com/ja/"
          target="_blank"
          rel="noopener noreferrer"
        >
          <vuetify-logo />
          <span class="text-capitalize">Made with Vuetify</span>
        </v-btn>
      </v-toolbar-items>
    </v-app-bar>

    <v-content>
      <v-container>
        <nuxt />
      </v-container>
    </v-content>

    <v-footer app>
      <span>&copy; 2019</span>
    </v-footer>
  </v-app>
</template>

<script>
import Logo from '~/components/Logo.vue'
import VuetifyLogo from '~/components/VuetifyLogo.vue'

export default {
  components: {
    Logo,
    VuetifyLogo
  },
  data () {
    return {
      title: 'Nuxt.js Advent Calendar 2019 for Qiita'
    }
  }
}
</script>
