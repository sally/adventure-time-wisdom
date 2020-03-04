<template>
    <div id="random-character-quote">
        <div class="card">
            <div class="card-content has-text-centered">
                <img :src="character.sprite" />
                <transition name="fade" mode="out-in">
                    <p :key="displayedQuoteIndex">{{ displayedQuote }}</p>
                </transition>
                <br />
                <p>
                    <button class="is-small button" @click="randomizeQuote">
                        More {{ character.displayName }} wisdom?
                    </button>
                </p>
            </div>

        </div>
    </div>
</template>

<script>
export default {
    name: 'random-character-quote',
    props: {
        character: Object
    },
    data() {
        return {
            displayedQuote: "",
            displayedQuoteIndex: -1
        }
    },
    methods: {
        randomizeQuote() {
            const availableQuotes = this.character.quotes.filter(quote => quote != this.displayedQuote);
            this.displayedQuote = availableQuotes[Math.floor(Math.random() * availableQuotes.length)];
            this.displayedQuoteIndex = this.character.quotes.indexOf(this.displayedQuote);
        }
    },
    created() {
        this.randomizeQuote();
    }
}
</script>

<style scoped>
    .fade-enter-active, .fade-leave-active {
        transition: opacity .25s;
    }
    .fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
        opacity: 0;
    }
</style>