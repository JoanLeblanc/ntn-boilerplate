<template>
  <main>
    <section v-if="posts" class="w-full max-w-5xl mx-auto">
      <picture>
        <img src='/assets/images/TRIO_PEX.jpg' alt="Photo du groupe Trio Liny">
      </picture>
      <h1 class="title">Trio liny</h1>
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
