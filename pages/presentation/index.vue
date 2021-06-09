<template>
  <main>
    <section v-if="posts" class="w-full max-w-5xl mx-auto">
      <h1 class="title">Présentation</h1>
      <posts post-type="presentation" :amount="10" />
    </section>
  </main>
</template>

<script>
export default {
  async asyncData({ $content, error }) {
    let posts;
    try {
      posts = await $content("presentation").fetch();
    } catch (e) {
      error({ message: "Presentation posts not found" });
    }
    return { posts };
  },
}
</script>
