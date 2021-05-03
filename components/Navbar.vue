<template>
  <div class="mb-4">
    <img src="../assets/images/logo.png" class="mx-auto" />
    <NuxtLink
      exact
      :to="{ name: 'index' }"
      class="text-primary font-bold hover:underline text-2xl px-3"
    >
      Blog
    </NuxtLink>
    <NuxtLink
      exact
      :to="{ name: 'about' }"
      class="font-bold hover:underline text-2xl px-3"
    >
      About
    </NuxtLink>
  </div>
</template>

<style>
a.nuxt-link-active {
  color: #81adf7;
}
</style>
