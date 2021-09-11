<template>
  <main>
    <section v-if="posts" class="w-full max-w-5xl mx-auto">
      <h1 class="title text-center">Agenda</h1>
      <h2  class="title text-center">Concert à venir</h2>
      <posts :dataSpeciale="postsFuturs" post-type="agenda" :amount="10" />
      <h2  class="title text-center">Concert passé</h2>
      <posts :dataSpeciale="postPasses" post-type="agenda" :amount="10" />

    </section>
  </main>
</template>

<script>
export default {
  async asyncData({ $content, error }) {
    let posts;
    let postsFuturs = [];
    let postPasses = [];
    const toDate = (dateStr) => {
      Date.prototype.addDays = function (days) {
        const date = new Date(this.valueOf());
        date.setDate(date.getDate() + days);
        return date;
      };
      const [day, month, year] = dateStr.split("/")
      const newDate =  new Date(year, month-1,day)
      return newDate.addDays(1)
    }
    try {
      posts = await $content("agenda").fetch();
      posts.forEach(concert => {
        if (toDate(concert.date) > new Date()) {
          postsFuturs.push(concert)
        } else {
          postPasses.push(concert)
        }
      })
      postsFuturs.sort((a,b)=> toDate(b.date) - toDate(a.date))
      postPasses.sort((a,b)=> toDate(b.date) - toDate(a.date))

    } catch (e) {
      error({ message: "agenda not found" });
    }

    return { posts, postsFuturs, postPasses };
  },
}
</script>
