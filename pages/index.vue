<template>
  <div class="flex flex-col">
    <div class="flex flex-col mx-auto text-center">
      <div class="links">
        <navbar></navbar>
      </div>

      <ul>
        <li
          v-for="article of articles"
          :key="article.slug"
          class="border border-gray-200 m-4 p-10 rounded text-left max-w-2xl bg-white"
        >
          <NuxtLink :to="{ name: 'blog-slug', params: { slug: article.slug } }">
            <img :src="article.img" />
            <div>
              <h2 style="color: #20887a" class="text-2xl font-bold mb-2 mt-4">
                {{ article.title }}
              </h2>
              <p style="color: #edbcab" class="text-sm font-semibold my-2">
                {{ formatDate(article.createdAt) }}
              </p>
              <p class="my-1">{{ article.description }}</p>
              <button style="color: #81adf7" class="my-2 font-bold underline">
                Read more
              </button>
            </div>
          </NuxtLink>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import moment from 'moment'
export default {
  async asyncData({ $content, params }) {
    const articles = await $content('articles')
      .only(['title', 'description', 'img', 'slug', 'author', 'createdAt'])
      .sortBy('createdAt', 'asc')
      .fetch()

    return {
      articles,
    }
  },
  methods: {
    formatDate(date) {
      return moment(date).format('MMMM Do YYYY')
    },
  },
}
</script>

<style></style>
