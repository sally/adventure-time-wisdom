<template>
    <div id="random-character-quote">
        <img :src="character.sprite" />
        <br/>
        {{ randomQuote }}
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