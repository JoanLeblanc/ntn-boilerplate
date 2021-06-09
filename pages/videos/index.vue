<template>
  <main>
    <section v-if="posts" class="w-full max-w-5xl mx-auto">
      <h1 class="title">Vidéos</h1>
      <posts post-type="video" :amount="10" />
    </section>
  </main>
</template>

<script>
export default {
  async asyncData({ $content, error }) {
    let posts;
    try {
      posts = await $content("video").fetch();
    } catch (e) {
      error({ message: "video not found" });
    }
    return { posts };
  },
}
</script>
