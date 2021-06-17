<template>
  <main>
    <section class="self-center flex flex-col flex-1 items-center justify-center">
      <h1 class="title text-center">Trio Liny</h1>
    </section>

    <section class="mt-8">
      <h3 class="text-primary-600 dark:text-primary-400 max-w-5xl mx-auto">Dernières actualités</h3>
      <posts post-type="agenda" :amount="1" />
    </section>
    <section class="mt-8">
      <h3 class="text-primary-600 dark:text-primary-400 max-w-5xl mx-auto">Dernières vidéos</h3>
      <posts post-type="video" :amount="1" />
    </section>
  </main>
</template>