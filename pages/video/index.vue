<template>
  <main>
    <section v-if="post" class="w-full max-w-5xl mx-auto">
      <h1 class="title text-center">Vidéos</h1>
      <posts post-type="video" :amount="10" />
    </section>
  </main>
</template>
<script>
export default {
  async asyncData({ $content, params, error }) {
    let post;
    try {
      post = await $content("video", params.video).fetch();
    } catch (e) {
      error({ message: "video not found" });
    }
    return { post };
  },
}
</script>

