<template>
  <div id="app">
    <section class="hero is-fullheight">
      <!-- <div class="hero-head">Hero Header Text</div> -->
      <div class="hero-body">
        <div class="container has-text-centered">
          <random-character-quote
            v-for="character in characters"
            :character="character"
            :key="character.slug"
          />
        </div>
      </div>
      <!-- <div class="hero-foot">Hero Header Footer</div> -->
    </section>
  </div>
</template>

<script>
import RandomCharacterQuote from './components/RandomCharacterQuote.vue'

export default {
  name: 'App',
  data() {
    return {
      characters: []
    }
  },
  components: {
    RandomCharacterQuote
  },
  methods: {
    fetchCharacters() {
      fetch("https://adventure-time-api.herokuapp.com/api/v1/characters", {
        method: 'GET'
      })
        .then(response => response.json())
        .then(json => this.characters = json)
    }
  },
  created() {
    this.fetchCharacters();
  }
}
</script>

<style>
@import '../node_modules/bulma/css/bulma.css';

#app {
  background-image: url("https://i.imgur.com/RETkwA5.png");
  background-color: rgba(255, 255, 255, 0.8);
  background-blend-mode: lighten;
}
</style>