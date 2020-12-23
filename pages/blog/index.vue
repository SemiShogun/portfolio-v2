<template>
  <main v-if="blogPosts" class="main">
    <div class="flex flex-col items-center justify-center rounded-md container-color text-white p-6">
      <!-- <logo /> -->
      <div class="flex flex-col w-5/6">
        <h1 class="flex flex-row justify-center text-3xl font-bold">Articles</h1>
        <ul v-for="(blogPost, index) in blogPosts" :key="index" class="articles">
          <nuxt-link :to="`blog/${blogPost.slug}`" class="article article--clickable">
            <div class="flex justify-between align-baseline items-center mt-5">
              <img class="object-cover h-16 w-16 border-2" :src="`${blogPost.seoMetaImage}`" alt="Blog Image" />
              <div class="flex flex-row justify-between items-center h-24 w-5/6">
                <h3 class="text-xl font-bold">{{ blogPost.title }}</h3>
                <h6 v-if="blogPost.date" class="bg-orange-400 rounded pl-2 pr-2 pt-1 pb-1">
                  {{ formatDate(blogPost.date) }}
                </h6>
              </div>
            </div>
          </nuxt-link>
        </ul>
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
