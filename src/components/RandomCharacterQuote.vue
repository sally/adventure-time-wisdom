<template>
    <div id="random-character-quote">
        <div class="card">
            <div class="card-content has-text-centered">
                <img :src="character.sprite" />
                <p>{{ displayedQuote }}</p>
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
            displayedQuote: ""
        }
    },
    methods: {
        randomizeQuote() {
            const availableQuotes = this.character.quotes.filter(quote => quote != this.displayedQuote);
            this.displayedQuote = availableQuotes[Math.floor(Math.random() * availableQuotes.length)];
        }
    },
    created() {
        this.randomizeQuote();
    }
}
</script>

<style scoped />