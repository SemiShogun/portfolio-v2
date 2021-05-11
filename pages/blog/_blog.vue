<template>
  <article v-if="blogPost" class="main article">
    <div class="flex flex-col items-center justify-center rounded-md container-color text-white p-6">
      <!-- <logo /> -->
      <div class="flex flex-col w-5/6">
        <div class="flex flex-row justify-center items-center">
          <img class="object-cover h-16 w-16 border-2" :src="`${blogPost.seoMetaImage}`" alt="Blog Image" />
          <h1 class="text-3xl font-bold ml-6">{{ blogPost.title }}</h1>
        </div>
        <div class="flex flex-col mt-5">
          <div v-html="$md.render(blogPost.body)"></div>
        </div>
        <hr class="rounded mt-6 mb-6 border-white border-b-2" />
        <div id="remark42"></div>
        <div class="flex flex-row justify-end">
          <h6 v-if="blogPost.date" class="bg-orange-400 rounded pl-2 pr-2 pt-1 pb-1">
            {{ formatDate(blogPost.date) }}
          </h6>
        </div>
      </div>
    </div>
  </article>
</template>
<script>
export default {
  async asyncData({ params, payload }) {
    if (payload) return { blogPost: payload }
    else
      return {
        blogPost: await require(`~/assets/content/blog/${params.blog}.json`),
      }
  },
  head() {
    return {
      script: [{ src: '~assets/js/remark42.js' }],
    }
  },
  methods: {
    formatDate(dateString) {
      const date = new Date(dateString)
      return date.toLocaleDateString(process.env.lang) || ''
    },
  },
}
</script>
