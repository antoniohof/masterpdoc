<template>
  <div class="mainpage">
    <div class="category" v-for="(c, index) in categories" :key="index">
      <span class="category_name">{{ c }}</span>
      <ColumnPosts
        class="category_content"
        :category="c"
        :posts="filteredPosts(c)"
      />
    </div>
    <!--
		<transition-group class="posts" id="posts" name="flip-list">
			<div v-for="(p) in searchedPosts" class="post" :key="p.slug">
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
    -->
  </div>
</template>

<script>
import { ColumnPosts } from "@/components";

export default {
  head() {
    return {
      script: [
        { src: "https://identity.netlify.com/v1/netlify-identity-widget.js" }
      ]
    };
  },
  components: {
    ColumnPosts
  },
  mounted() {},
  data() {
    return {
      searchValue: "",
      colors: ["#000000"], //, '#4B0082', '#0000FF', '#00FF00', '#ff0066', '#FF7F00', '#FF0000'],
      tags: [],
      categories: [
        "Broad Research",
        "Theory",
        "Ideas",
        "References",
        "Technical",
        "Sketches",
        "Project"
      ]
    };
  },
  computed: {
    searchedPosts() {
      if (this.searchValue !== "") {
        return this.posts.filter(post => {
          return (
            this.searchValue
              .toLowerCase()
              .split(" ")
              .every(v => post.title.toLowerCase().includes(v)) ||
            this.searchValue
              .toLowerCase()
              .split(" ")
              .every(v => post.description.toLowerCase().includes(v))
          );
        });
      } else {
        return this.posts;
      }
    }
  },
  async asyncData({ $content }) {
    const posts = await $content("blog").fetch();
    return {
      posts
    };
  },
  methods: {
    getRandomInt(min, max) {
      min = Math.ceil(min);
      max = Math.floor(max);
      return Math.floor(Math.random() * (max - min)) + min;
    },
    getTranslation(p) {
      if (p.translation) {
        return p.translation;
      }
      let translation =
        "translate(" +
        this.getRandomInt(-15, 15) +
        "px," +
        this.getRandomInt(-15, 15) +
        "px) !important";
      p.translation = translation;
      return translation;
    },
    getColor(p) {
      if (p.color) {
        return p.color;
      }
      let color =
        this.colors[this.getRandomInt(0, this.colors.length)] + " !important";
      p.color = color;
      return color;
    },
    countTags() {
      let concatenatedTags = "";
      for (let i = 0; i < this.searchedPosts.length; i++) {
        if (this.searchedPosts[i].tags) {
          if (i != 0) {
            concatenatedTags += ",";
          }
          concatenatedTags += this.searchedPosts[i].tags;
        }
      }
      this.tags = concatenatedTags.split(",");
    },
    filteredPosts(c) {
      return this.searchedPosts.filter(p => {
        return p.category && p.category.includes(c) > 0;
      });
    }
  },
  watch: {}
};
</script>

<style scoped lang="sass">
.mainpage
	display: flex
	flex-flow: row
	height: 100%
	width: fit-content
	align-items: center
	overflow-x: scroll
	justify-content: space-evenly
	align-items: flex-start
	.category
		border-right: 1px solid black
		padding: 10px
		&_name
			color: black
			font-size: 20px
			font-weight: 600
		&_content
			margin-top: 20px
</style>
