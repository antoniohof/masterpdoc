<template>
  <div>
		<transition-group class="posts" id="posts" name="flip-list">
			<div v-for="(p, index) in searchedPosts" class="post" :key="index">
        <NuxtLink :to="p.slug" class="post_body" :style="{ 'transform': getTranslation(p), 'background-color': getColor(p) }">
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
  head () {
    return {
      script: [{ src: 'https://identity.netlify.com/v1/netlify-identity-widget.js' }]
    }
  },
  data () {
    return {
      searchValue: '',
      colors: ['#000000'] //, '#4B0082', '#0000FF', '#00FF00', '#ff0066', '#FF7F00', '#FF0000'],
    }
  },
  computed: {
    searchedPosts () {
        if(this.searchValue !== '') {
          return this.posts.filter((post) =>  {
            return this.searchValue.toLowerCase().split(' ').every(v => post.title.toLowerCase().includes(v)) || this.searchValue.toLowerCase().split(' ').every(v => post.description.toLowerCase().includes(v))
          })
        } else {
          console.log(this.posts)
          return this.posts
        }
      }
  },
  components: {
  },
  async asyncData({ $content }) {
    const posts = await $content("blog").fetch()

    return {
      posts
    }
  },
  methods: {
    getRandomInt (min, max) {
      min = Math.ceil(min);
      max = Math.floor(max);
      return Math.floor(Math.random() * (max - min)) + min;
    },
    getTranslation (p) {
      if (p.translation) {
        return p.translation
      }
      let translation = 'translate(' + this.getRandomInt(-15, 15) + 'px,' + this.getRandomInt(-15, 15) + 'px) !important'
      p.translation = translation
      return translation
    },
    getColor (p) {
      if (p.color) {
        return p.color
      }
      let color = this.colors[this.getRandomInt(0, this.colors.length)] + ' !important'
      p.color = color
      return color
    },
  }
}
</script>

<style scoped>
.posts {
	display: flex;
	flex-flow: column wrap;
	max-height: 100vh;
	height: calc(100vh - 115px);
	position: fixed;
	left: 5px;
	top: 5px;
	align-items: center;
	overflow-y: hidden;
	width: 100vw;
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
  max-width: 200px;
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
  transform: translateX(200px);
}

</style>
