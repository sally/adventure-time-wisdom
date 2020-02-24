<template>
  <div id="app">
    <section class="hero is-fullheight">
      <!-- <div class="hero-head">Hero Header Text</div> -->
      <div class="hero-body">
        <div class="container has-text-centered">
          <random-quote testMsg="A mathematical quote here!"/>
        </div>
      </div>
      <!-- <div class="hero-foot">Hero Header Footer</div> -->
    </section>
  </div>
</template>

<script>
import RandomQuote from './components/RandomQuote.vue'

export default {
  name: 'App',
  components: {
    RandomQuote
  }
}
</script>

<style>
@import '../node_modules/bulma/css/bulma.css';

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background-image: url("https://i.imgur.com/RETkwA5.png");
  background-color: rgba(255, 255, 255, 0.8);
  background-blend-mode: lighten;
}
</style>