<template>
  <main v-if="blogPosts" class="main">
    <div class="flex flex-col items-center justify-center rounded-md container-color text-white p-6">
      <!-- <logo /> -->
      <div class="flex flex-col w-5/6">
        <div class="font-light">
          <ul v-for="(blogPost, index) in blogPosts" :key="index" class="articles">
            <nuxt-link :to="`blog/${blogPost.slug}`" class="article article--clickable">
              <div class="flex justify-between align-baseline">
                <h3 class="article-title">{{ blogPost.title }}</h3>
                <h6
                  v-if="blogPost.date"
                  class="inline-block py-1 px-2 bg-accent text-white font-medium rounded-sm dark:bg-accent whitespace-no-wrap"
                >
                  {{ formatDate(blogPost.date) }}
                </h6>
              </div>
              <div class="mt-4 mb-2">
                <p class="inline">{{ blogPost.description }}</p>
              </div>
            </nuxt-link>
          </ul>
        </div>
        <div class=""></div>
      </div>
    </div>
  </main>
</template>
<script>
export default {
  computed: {
    blogPosts() {
      return this.$store.state.blogPosts
    },
  },
  methods: {
    formatDate(dateString) {
      const date = new Date(dateString)
      return date.toLocaleDateString(process.env.lang) || ''
    },
  },
}
</script>
