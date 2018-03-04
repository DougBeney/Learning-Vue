<template lang="pug">
show-blogs
</template>

<script>
import addBlog from './components/addBlog.vue'
import showBlogs from './components/showBlogs.vue'

export default {
	components: {
		"add-blog": addBlog,
		"show-blogs": showBlogs
	},
	data() {
		return {

		}
	}
}
</script>

<style lang="sass">
</style>
