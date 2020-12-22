<template>
  <div id="header">
    <ul class="flex flex-col justify-items-start wx-12 text-white">
      <li class="flex-1 p-1 font-bold text-5xl">
        <nuxt-link class="btn block" to="/">Nectoj</nuxt-link>
      </li>
      <li class="flex-1 p-1 font-light text-3xl">
        <nuxt-link class="btn block" to="/blog">Blog</nuxt-link>
      </li>
      <li class="flex-1 p-1 font-light text-3xl">
        <a href="https://github.com/SemiShogun">Github</a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Header',
}
</script>

<style scoped>
</style>
