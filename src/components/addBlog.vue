<template lang="pug">
#add_blog
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


	.column
		#preview
			h3 Preview
			hr
			h1 {{blog.title}}
			small
				| Categories: 
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
				author: "Default"
			},
			authors: ["Doug", "Andrew", "Ryan", "Andy"]
		}
	}
}
</script>

<style lang="sass">
#add_blog
	max-width: 1080px
	margin: 0 auto
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
