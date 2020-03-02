<template>
    <div id="random-character-quote">
        <div class="card">
            <div class="card-content has-text-centered">
                <img :src="character.sprite" />
                <br/>
                {{ randomQuote }}
            </div>
            <footer class="card-footer">
                <p class="card-footer-item">{{ character.displayName }}</p>
            </footer>
        </div>
    </div>
</template>

<script>
export default {
    name: 'random-character-quote',
    props: {
        character: Object
    },
    computed: {
        randomQuote() {
            return this.character.quotes[Math.floor(Math.random() * this.character.quotes.length)];
        }
    }
}
</script>

<style scoped />