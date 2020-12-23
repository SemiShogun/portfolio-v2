<template>
  <main class="main">
    <div class="flex flex-col items-center rounded-md container-color text-white p-6">
      <template v-if="error.statusCode === 404">
        <h1 class="text-3xl font-bold">Page Not Found</h1>
        <h2 class="text-xl subtitle mb-2">404</h2>
        <p class="text-lg mb-4">
          Looks like you've followed a broken link or entered a URL that doesn't exist on this site.
        </p>
      </template>
      <template v-else>
        <h1 class="text-3xl font-bold">An error occurred</h1>
        <p class="text-lg mb-4">
          Looks like you've followed a broken link or entered a URL that doesn't exist on this site.
        </p>
      </template>
      <img class="object-cover h-2/6 w-2/6 border-2 m-4" src="../static/charlotte_404.gif" alt="Error 404" />
      <nuxt-link to="/">
        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 16 16" class="inline fill-current">
          <path
            d="M11.9998836,4.09370803 L8.55809517,7.43294953 C8.23531459,7.74611298 8.23531459,8.25388736 8.55809517,8.56693769 L12,11.9062921 L9.84187871,14 L4.24208544,8.56693751 C3.91930485,8.25388719 3.91930485,7.74611281 4.24208544,7.43294936 L9.84199531,2 L11.9998836,4.09370803 Z"
          ></path>
        </svg>
        Go back
      </nuxt-link>
    </div>
  </main>
</template>

<script>
export default {
  name: 'error',
  props: ['error'],
}
</script>
