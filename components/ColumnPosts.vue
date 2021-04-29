<template>
  <div>
		<transition-group class="posts" id="posts" name="flip-list">
			<div v-for="(p) in posts" class="post" :key="p.slug">
        <NuxtLink :to="p.slug" class="post_body">
          <a :href="p.link">
            <h3 class="post_title">{{ p.title }}</h3>
            <div class="post_excerpt">{{ p.description }}</div>
            <div v-if='p.thumbnail' class="post_thumbnail">
              <img class="post_thumbnail_img" :src='p.thumbnail'/>
            </div>
          </a>
			  </NuxtLink>
			</div>
		</transition-group>
  </div>
</template>

<script>
export default {
  name: 'ColumnPosts',
  props: {
    posts: {
      type: Array,
      default: [],
      required: true
    }
  },
  mounted () {

  },
  data () {
    return {
    }
  },
  computed: {

  },
  components: {
  },
  methods: {

  },
  watch: {
  }
}
</script>

<style scoped>
.posts {
	display: flex;
	flex-flow: column;
	height: 100%;
	left: 5px;
	top: 5px;
	align-items: center;
	overflow-x: hidden;
	width: 100%;
	justify-content: space-evenly;
	z-index: 0;
	filter: drop-shadow(2px 4px 6px black);
}


.post{
  cursor: pointer;
	display: flex;
	max-width: 500px;
	max-height: 300px;
	height: fit-content;
	margin: 1px;
  display: flex;
  align-items: center;
  transition: 0.4s ease;
  margin-bottom: 20px;
}

.post:hover{
	transition: 0.4s ease;
	transform: scale(1.08);
	z-index: 9999;
}

.post_body {
  color: white !important;
  background-color: black;
  text-decoration: none !important;
	width: 100%;
}

.post_title {
	font-size: 14px;
	color: white !important;
	margin: 10px;
	margin-bottom: 10px !important;
}

.post_excerpt {
	font-family: 'Roboto Mono', monospace !important;
	font-size: 10px !important;
	margin: 10px;
	text-decoration: none !important;
	color: white !important;
}

.post_thumbnail {
	font-family: 'Roboto Mono', monospace !important;
	font-size: 10px !important;
	margin: 10px;
	text-decoration: none !important;
	color: white !important;
}

.post_thumbnail_img {
  max-width: 100px;
}

a:hover, a:visited, a:link, a:active
{
    text-decoration: none !important;
}

.flip-list-move {
  transition: transform 0.5s ease;
}

.flip-list-move {
  transition: transform 0.5s ease;
}

.flip-list-enter-active, .flip-list-leave-active {
  transition: all 0.5s;
}
.flip-list-enter, .flip-list-leave-to /* .list-leave-active below version 2.1.8 */ {
  opacity: 0;
  transform: translateY(200px);
}

</style>
