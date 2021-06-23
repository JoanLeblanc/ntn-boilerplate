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
        <h1 class="text-center">{{ post.title }}</h1>
        <div class="container m-t-20">
          <iframe class="responsive-iframe" :src="post.lien_video"></iframe>
        </div>
        <div>
            <h6 class="italic m-t-20">Plus d'informations: </h6>
            <nuxt-content :document="post" />
        </div>

      </article>
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
