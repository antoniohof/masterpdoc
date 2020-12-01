<template>
  <v-app dark>
    <v-main>
      <v-container fluid>
        <nuxt />
      </v-container>
    </v-main>
    <!--
    <v-footer
      absolute
      app
    >
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
    -->
  </v-app>
</template>

<script>
export default {
  mounted () {
    console.log('mounted app')
  },
  data () {
    return {
    }
  }
}
</script>
