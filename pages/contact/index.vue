<template>
  <main>
    <section class="self-center flex flex-col flex-1 items-center justify-center">
      <h1 class="title text-center">Form Contact</h1>
    <form name="contact" method="POST" data-netlify="true">
        <p>
            <label>Votre Nom: <input type="text" name="name" /></label>   
        </p>
        <p>
            <label>Votre Email: <input type="email" name="email" /></label>
        </p>
        <p>
            <label>Message: <textarea name="message"></textarea></label>
        </p>
        <p>
            <button type="submit">Envoyez</button>
        </p>
    </form>
    </section>
  </main>
</template>