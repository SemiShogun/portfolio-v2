<template>
  <div class="flex flex-col items-center justify-center rounded-md container-color text-white p-6">
    <!-- <logo /> -->
    <div class="flex flex-col w-5/6">
      <h1 class="flex flex-row justify-center text-3xl font-bold">About Myself</h1>
      <p>
        Hello everyone! NectoJ here. I’m a developer from the snowy alps of Zürich, Switzerland. I have a fond interest
        when it comes to learning programming, technologies, tools and especially JS/TS frameworks. You’ll discover some
        of my various blog posts on this website regarding my current projects, ideas, reviews, writings, et cetera.
      </p>
      <h1 class="flex flex-row justify-center text-3xl font-bold">Current Projects</h1>
      <div></div>
    </div>
  </div>
</template>

<script>
// import Logo from '~/components/Logo.vue'

export default {
  // components: {
  //   Logo
  // },
  head() {
    return {
      script: [{ src: 'https://identity.netlify.com/v1/netlify-identity-widget.js' }],
    }
  },
}
</script>
