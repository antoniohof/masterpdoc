<template>
  <v-app>
    <v-main :class="{ index: $route.path === '/' }">
      <nuxt />
    </v-main>
  </v-app>
</template>

<script>
export default {
  mounted() {
    console.log("mounted app");
  },
  data() {
    return {};
  }
};
</script>

<style lang="sass">
*
	font-family: 'Helvetica', monospace !important

img
	max-width: 60vw
	margin: 0 auto
.v-main
	&.index
		max-width: none !important
		overflow-x: scroll !important
		width: 100%
</style>
