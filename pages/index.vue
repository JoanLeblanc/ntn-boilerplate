<template>
  <main>
    <section>
      <article>
        <div>
            <h1 class="title text-center">Trio Ligny</h1>
            <p>Touchant, surprenant, sensible, le Trio Ligny vous emmène dans un univers musical sublimé par le mariage du violon, du cor et du piano.</p>
            <p>De Mozart à John Williams, en passant par l’incontournable trio de Brahms, le Trio Ligny saura vous amener dans un voyage musical plein de romantisme et de surprise.</p>
            <div class="container m-t-40">
              <iframe class="responsive-iframe" src="https://www.youtube.com/embed/QPFz7lEHGVY"></iframe>
            </div>
        </div>


      </article>
    </section>

    <section class="mt-8">
      <div>
        <h3 class="subtitle text-center text-primary-600 dark:text-primary-400 max-w-5xl mx-auto">Actualités</h3>
        <a href="/agenda"><p class="text-center"> Toutes les actualités</p></a>
      </div>
      <posts :dataSpeciale="prochainConcert" :sortBy="{key: 'date', direction: 'desc'}" post-type="agenda" :amount="1" />
    </section>
    <section class="mt-8">
      <div>
        <h3 class="subtitle text-center text-primary-600 dark:text-primary-400 max-w-5xl mx-auto">Dernières vidéos</h3>
        <a href="/video"><p class="text-center"> Toutes les vidéos</p></a>

      </div>
      <posts post-type="video" :amount="1" />
    </section>
  </main>
</template>

<script>
export default {
  async asyncData({ $content, error }) {
    let posts;
    let prochainConcert = [];
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
          prochainConcert.push(concert)
        }
      })
      prochainConcert.sort((a,b)=> toDate(b.date) - toDate(a.date))
    } catch (e) {
      error({ message: "agenda not found" });
    }

    return { posts, prochainConcert };
  },
}
</script>