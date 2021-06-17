<template>
  <main>
    <section>
      <article>
        <div>
            <h1 class="title text-center">Trio Ligny</h1>
            <p>/Message Presentation/ Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
            <div class="container">
              <iframe class="responsive-iframe" src="https://www.youtube.com/embed/QPFz7lEHGVY"></iframe>
            </div>
        </div>


      </article>
    </section>

    <section class="mt-8">
      <h3 class="subtitle text-center text-primary-600 dark:text-primary-400 max-w-5xl mx-auto">Actualités</h3>
      <posts post-type="agenda" :amount="1" />
    </section>
    <section class="mt-8">
      <h3 class="subtitle text-center text-primary-600 dark:text-primary-400 max-w-5xl mx-auto">Dernières vidéos</h3>
      <posts post-type="video" :amount="1" />
    </section>
  </main>
</template>