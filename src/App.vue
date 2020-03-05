<template>
  <div id="app">
    <section class="header">
      <div class="columns has-text-centered">
        <div class="column is-one-third is-offset-one-third">
          <img src="./assets/header-at-logo.png">
          <br/>
          <h1 class="title">Adventure Time Wisdom</h1>
          <h1 class="subtitle">Inspirational, insightful <s>nonsense</s> quotes from the widely beloved children's show, Adventure Time.</h1>
        </div>
      </div>
    </section>
    <div class="has-text-centered" v-if="!dataFetched">
      <!-- CSS loading spinner -->
      <div class="lds-ring"><div></div><div></div><div></div><div></div></div>
    </div>
    <transition-group
      v-else
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
    <footer class="footer">
      <div class="content has-text-centered">
        <p>
          <a href="https://github.com/sally/adventure-time-wisdom">Adventure Time Wisdom</a> by Sally 🥰<br/>
          <i>Adventure Time</i> © Cartoon Network 📺
        </p>
      </div>
    </footer>
  </div>
</template>

<script>
import Velocity from 'velocity-animate'

import RandomCharacterQuote from './components/RandomCharacterQuote.vue'

export default {
  name: 'App',
  data() {
    return {
      characters: [],
      dataFetched: false
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
        .then(json => {
          this.characters = json;
          this.dataFetched = true;
        })
    },
    beforeEnter: el => el.style.opacity = 0,
    enter: (el, done) => {
      var delay = el.dataset.index * 250
      setTimeout(() => {
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
  background-image: url("./assets/bg-chars-breakfasts.png");
  background-color: rgba(255, 255, 255, 0.8);
  background-blend-mode: lighten;
}

.quotes-container {
  max-width: 1200px;
  margin: 0 auto;
}

.footer {
  background-color: transparent;
}

/* CSS loading spinner */
.lds-ring {
  display: inline-block;
  position: relative;
  width: 80px;
  height: 80px;
}
.lds-ring div {
  box-sizing: border-box;
  display: block;
  position: absolute;
  width: 64px;
  height: 64px;
  margin: 8px;
  border: 8px solid #fff;
  border-radius: 50%;
  animation: lds-ring 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
  border-color: #fff transparent transparent transparent;
}
.lds-ring div:nth-child(1) {
  animation-delay: -0.45s;
}
.lds-ring div:nth-child(2) {
  animation-delay: -0.3s;
}
.lds-ring div:nth-child(3) {
  animation-delay: -0.15s;
}
@keyframes lds-ring {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>