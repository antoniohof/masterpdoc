<template>
  <v-app>
    <v-main>
      <v-container fluid>
        <nuxt />
      </v-container>
    </v-main>
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
