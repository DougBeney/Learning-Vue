<template lang="pug">
.show-blogs(v-theme="'wide'")
	h1 All Blog Articles
	ul: li(v-for="post in posts")
		h1(v-rainbow="") {{post.title}}
</template>

<script>
export default {
	data() {
		return {
			posts: []
		}
	},
	methods: {

	},
	created() {
		this.$http.get("https://jsonplaceholder.typicode.com/posts").then(function(data) {
			console.log(data)
			this.posts = data.body.slice(0,10)
		})
	}
}
</script>

<style lang="sass">
	
</style>
