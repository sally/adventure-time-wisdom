<template>
  <div id="app">
    <section class="header">
      <div class="columns has-text-centered">
        <div class="column is-one-third is-offset-one-third">
          <img src="https://www.stickpng.com/assets/images/5c80f70f72f5d9028c17ed26.png">
          <br/>
          <h1 class="title">Adventure Time Wisdom</h1>
          <h1 class="subtitle">Inspirational, insightful <s>nonsense</s> quotes from the widely beloved children's show, Adventure Time.</h1>
        </div>
      </div>
    </section>
    <transition-group
      tag="div"
      class="quotes-container columns is-multiline"

      appear
      name="staggered-fade"
      v-bind:css="false"
      v-on:before-enter="beforeEnter"
      v-on:enter="enter"
    >
      <random-character-quote
        class="column is-one-third"
        v-for="(character, index) in characters"
        :character="character"
        :key="character.slug"
        :data-index="index"
      />
    </transition-group>
  </div>
</template>

<script>
import Velocity from 'velocity-animate'

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
    },
    beforeEnter: function (el) {
      el.style.opacity = 0;
    },
    enter: function (el, done) {
      var delay = el.dataset.index * 300
      setTimeout(function () {
        Velocity(
          el,
          { opacity: 1 },
          { complete: done }
        )
      }, delay)
    },
  },
  created() {
    this.fetchCharacters();
  }
}
</script>

<style>
@import '../node_modules/bulma/css/bulma.css';

html {
  background-image: url("https://i.imgur.com/RETkwA5.png");
  background-color: rgba(255, 255, 255, 0.8);
  background-blend-mode: lighten;
}

.quotes-container {
  max-width: 1200px;
  margin: 0 auto;
}
</style>