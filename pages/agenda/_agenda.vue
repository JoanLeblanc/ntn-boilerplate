<template>
  <main>
    <section v-if="post">
      <nav class="mb-8" aria-label="go back">
        <router-back class="block" />
      </nav>

      <article>
        <img
          v-if="post.cover"
          class="cover-image"
          :src="post.cover"
        >
        <!-- <h6 class="inline py-1 px-2 mr-1 bg-gray text-white text-sm font-medium rounded-sm">{{ post.category }}</h6> -->
        <h1 class="">{{ post.title }} : le {{ post.date}}</h1>
        <p class="mt-1 mb-8 text-primary-600 dark:text-primary-400">{{ post.description }}</p>
        <nuxt-content :document="post" />
      </article>
    </section>
  </main>
</template>

<script>
export default {
  async asyncData({ $content, params, error }) {
    let post;
    try {
      post = await $content("agenda", params.agenda).fetch();
    } catch (e) {
      console.error(e)
      error({ message: "agenda not found" });

    }
    return { post };
  },
}
</script>
