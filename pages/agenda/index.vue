<template>
  <main>
    <section v-if="posts" class="w-full max-w-5xl mx-auto">
      <h1 class="title text-center">Agenda</h1>
      <posts post-type="agenda" :amount="10" />
    </section>
  </main>
</template>

<script>
export default {
  async asyncData({ $content, error }) {
    let posts;
    try {
      posts = await $content("agenda").fetch();
    } catch (e) {
      error({ message: "agenda not found" });
    }
    return { posts };
  },
}
</script>
