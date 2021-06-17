<template>
  <main>
    <section v-if="posts" class="w-full max-w-5xl mx-auto">
      <h1 class="title">Video</h1>
      <posts post-type="video" :amount="10" />
    </section>
  </main>
</template>
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
