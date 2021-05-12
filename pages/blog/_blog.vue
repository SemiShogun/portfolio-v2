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
  methods: {
    formatDate(dateString) {
      const date = new Date(dateString)
      return date.toLocaleDateString(process.env.lang) || ''
    },
  },
  mounted() {
    var remark_config = {
      host: 'https://remark42.nectoj.ninja',
      // hostname of remark server, same as REMARK_URL in backend config,
      // e.g. "https://demo.remark42.com" site_id: 'remark42.vidal-rosset.net',components: ['embed', 'last-comments', 'counter'],
      // optional param; which components to load. default to ["embed"]
      // to load all components define components as ['embed', 'last-comments', 'counter']
      // available component are:
      //     - 'embed': basic comments widget
      //     - 'last-comments': last comments widget, see `Last Comments` section below
      //     - 'counter': counter widget, see `Counter` section below
      // url: '', // optional param; if it isn't defined
      // `window.location.origin + window.location.pathname` will be used,
      //
      // Note that if you use query parameters as significant part of url
      // (the one that actually changes content on page)
      // you will have to configure url manually to keep query params, as
      // `window.location.origin + window.location.pathname` doesn't contain query params and
      // hash. For example default url for `https://example/com/example-post?id=1#hash`
      // would be `https://example/com/example-post`.
      //
      // The problem with query params is that they often contain useless params added by
      // various trackers (utm params) and doesn't have defined order, so Remark treats differently
      // all this examples:
      // https://example.com/?postid=1&date=2007-02-11
      // https://example.com/?date=2007-02-11&postid=1
      // https://example.com/?date=2007-02-11&postid=1&utm_source=google
      //
      // If you deal with query parameters make sure you pass only significant part of it
      // in well defined order
      max_shown_comments: 10, // optional param; if it isn't defined default value (15) will be used
      theme: 'light', // optional param; if it isn't defined default value ('light') will be used
      // page_title: '' // optional param; if it isn't defined `document.title` will be used
    }

    ;(function (c) {
      for (var i = 0; i < c.length; i++) {
        var d = document,
          s = d.createElement('script')
        s.src = remark_config.host + '/web/' + c[i] + '.js'
        s.defer = true
        ;(d.head || d.body).appendChild(s)
      }
    })(remark_config.components || ['embed', 'last-comments', 'counter'])
  },
}
</script>
