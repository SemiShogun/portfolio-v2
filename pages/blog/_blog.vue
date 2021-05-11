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
      host: 'https://remark42.nectoj.ninja/', // hostname of remark server, same as REMARK_URL in backend config, e.g. "https://demo.remark42.com"
      site_id: 'JamieLam1234',
      components: ['embed'], // optional param; which components to load. default to ["embed"]
      // to load all components define components as ['embed', 'last-comments', 'counter']
      // available component are:
      //     - 'embed': basic comments widget
      //     - 'last-comments': last comments widget, see `Last Comments` section below
      //     - 'counter': counter widget, see `Counter` section below
      //   url: 'PAGE_URL', // optional param; if it isn't defined
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
      theme: 'dark', // optional param; if it isn't defined default value ('light') will be used
      page_title: 'Moving to Remark42', // optional param; if it isn't defined `document.title` will be used
      locale: 'en', // set up locale and language, if it isn't defined default value ('en') will be used
      show_email_subscription: false, // optional param; by default it is `true` and you can see email subscription feature
      // in interface when enable it from backend side
      // if you set this param in `false` you will get notifications email notifications as admin
      // but your users won't have interface for subscription
    }

    ;(function () {
      var host = 'https://remark42.nectoj.ninja/' // Your remark42 host
      var components = ['embed'] // Your choice of remark42 components

      ;(function (c) {
        for (let i = 0; i < c.length; i++) {
          const d = document
          const s = d.createElement('script')
          s.src = host + '/web/' + c[i] + '.js'
          s.defer = true
          ;(d.head || d.body).appendChild(s)
        }
      })(components)
    })
  },
}
</script>
