<template lang="pug">
#add_blog
	.message(v-if="blog.published") Successfully Published!
	.column
		h1.title Add New Post
		form
			label Title
			input(v-model="blog.title", type="text" required="")

			label Content
			textarea(v-model="blog.content", )

			label Categories
			#checkboxes
				input(type="checkbox", value="Roundups", v-model="blog.categories")
				label Roundups
				input(type="checkbox", value="Recipes", v-model="blog.categories")
				label Recipes
			
			label Author
			select(v-model="blog.author")
				option(v-for="author in authors") {{author}}
			button(@click.prevent="publish") Publish

	.column
		#preview
			h1.title Preview
			h1 {{blog.title}}
			h1(v-if="blog.title == ''") Untitled
			small
				| Categories: 
				span(v-if="blog.categories.length == 0") Uncategorized
				template(v-for="category, index in blog.categories")
					| {{category}}
					template(v-if='blog.categories.length-1 != index')
						| , 
			br
			small written by {{blog.author}}
			#blog_content(v-html="compiledMarkdown")
</template>

<script>
export default {
	computed: {
		compiledMarkdown() {
			return marked(this.blog.content)
		}
	},
	data() {
		return {
			blog: {
				title: "",
				content: "",
				categories: [],
				author: "Anon",
				published: false
			},
			authors: ["Doug", "Andrew", "Ryan", "Andy"]
		}
	},
	methods: {
		publish() {
			this.$http.post('https://jsonplaceholder.typicode.com/posts', {
				title: this.blog.title,
				body: this.blog.content,
				userId: 1
			}).then(function(data) {
				console.log(data)
				this.blog.published = true
			})
		}
	},
}
</script>

<style lang="sass">
#add_blog
	max-width: 1080px
	margin: 0 auto

	.message
		background: lightgreen
		border: 1px dotted green
		padding: 15px
		text-align: center
	.column
		width: 50%
		display: inline
		float: left
		box-sizing: border-box
		padding: 15px
	h1.title
		text-align: center
		text-transform: uppercase
		letter-spacing: 2px
		font-weight: 200
	form
		*
			margin: 15px 0
		input, textarea, button
			display: block
			box-sizing: border-box
			padding: 15px
			width: 100%
		textarea
			min-height: 400px
		#checkboxes
			display: block
			input, textarea, button
				width: auto
				padding: 0
				display: inline

</style>
