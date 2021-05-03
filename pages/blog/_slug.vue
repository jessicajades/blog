<template>
  <div>
    <div class="flex flex-col mx-auto text-center">
      <navbar></navbar>
    </div>

    <article class="flex items-center justify-center flex-col mt-8 p-3 sm:p-0">
      <div class="max-w-3xl bg-white p-6 mb-8 rounded border border-gray-200">
        <h1 class="text-3xl font-semibold">{{ article.title }}</h1>
        <p class="mt-2">
          Article last updated: {{ formatDate(article.updatedAt) }}
        </p>
        <img class="rounded mt-4" :src="article.img" :alt="article.alt" />

        <nav>
          <ul>
            <li v-for="link of article.toc" :key="link.id">
              <NuxtLink :to="`#${link.id}`" class="bg-pink-100">{{
                link.text
              }}</NuxtLink>
            </li>
          </ul>
        </nav>

        <nuxt-content :document="article" />

        <author></author>

        <prev-next class="mb-2" :prev="prev" :next="next" />
      </div>
    </article>
  </div>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    const article = await $content('articles', params.slug).fetch()

    const [prev, next] = await $content('articles')
      .only(['title', 'slug'])
      .sortBy('createdAt', 'asc')
      .surround(params.slug)
      .fetch()

    return { article, prev, next }
  },
  methods: {
    formatDate(date) {
      const options = { year: 'numeric', month: 'long', day: 'numeric' }
      return new Date(date).toLocaleDateString('en', options)
    },
  },
}
</script>

<style scoped>
.nuxt-content p {
  margin-bottom: 200px;
}
</style>
