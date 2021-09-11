<template>
  <ul v-if="posts.length > 0" class="cards">
    <li
      v-for="(post, index) in posts"
      :key="index"
    >
      <nuxt-link
        :to="`${postType}/${post.slug}`"
        class="card card--clickable"
      >
        <template v-if="postType === 'video'">
          <span class="flex-1">
            <h3 class="card-title text-center">{{ post.title }}</h3>
            <div class="post-video container m-t-20">
              <iframe class="responsive-iframe" :src="post.lien_video"></iframe>
            </div>
          </span>
          <img
            v-if="post.cover"
            class="cover-image"
            :src="post.cover"
          >
        </template>

        <template v-else>
          <span class="w-full">
            <span class="flex justify-between align-baseline">
              <h3 class="card-title ">{{ post.title }}</h3>
              <h6
                v-if="post.date"
                class="self-start inline-block mt-0 py-1 px-2 bg-gray text-white text-base font-medium rounded-sm whitespace-no-wrap"
              >{{ post.date }}</h6>
            </span>
            <p class="mt-2">{{ post.description }}</p>
          </span>
        </template>
      </nuxt-link>
    </li>
  </ul>
  <div v-else-if="loading" class="cards">
    <div v-for="placeholder in placeholderClasses" :key="placeholder.id" class="card">
      <content-placeholders :rounded="true" :class="placeholder">
        <content-placeholders-heading />
      </content-placeholders>
    </div>
  </div>
  <p v-else class="max-w-5xl mx-auto">
    {{ amount > 1 ? 'Posts not found' : 'Post not found' }}
  </p>
</template>

<script>
  export default {
    name: 'Posts',
    props: {
      postType: {
        type: String,
        default: 'video',
        validator: (val) => ['agenda', 'video'].includes(val),
      },
      amount: { // ? https://content.nuxtjs.org/fetching#limitn
        type: Number,
        default: 10,
        validator: (val) => val >= 0 && val < 100,
      },
      sortBy: { // ? https://content.nuxtjs.org/fetching#sortbykey-direction
        type: Object,
        default: () => ({
          key: 'slug',
          direction: 'desc' // you probably want 'asc' here
        }),
        validator: (obj) => typeof obj.key === 'string' && typeof obj.direction === 'string',
      },
      where: {
        type: Object,
        default: () => ({ }),
      },
      dataSpeciale: {
        type: Array,
      }
    },
    data() {
      return {
        posts: [],
        loading: true,
      }
    },
    computed: {
      placeholderClasses() {
        const classes = ['w-full','w-2/3','w-5/6'];
        return [...Array.from({ length: this.amount }, (v, i) => classes[i % classes.length])]; // repeats classes after one another
      }
    },
    async mounted() {
      this.loading = true;
      this.posts = await this.fetchPosts();
      this.loading = false;
    },
    methods: {
      formatDate(dateString) {
        const date = new Date(dateString)
        return date.toLocaleDateString(process.env.lang) || ''
      },
      toDate(dateStr) {
        const [day, month, year] = dateStr.split("/")
        return new Date(year, month - 1, day + 1 )
      },
      async fetchPosts(
          dataSpeciale = this.dataSpeciale,
          where = this.where,
          postType = this.postType,
          amount = this.amount,
          sortBy = this.sortBy,
        ) {

          if(dataSpeciale && dataSpeciale.length > 0) {
            return dataSpeciale
          }
        return this.$content(postType)
          .sortBy(sortBy.key, sortBy.direction)
          .limit(amount)
          .fetch()
          .catch((err) => {
            error({ statusCode: 404, message: amount > 1 ? 'Posts not found' : 'Post not found' })
          });
      }
    },
  }
</script>
