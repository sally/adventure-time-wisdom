<template>
    <span>{{ character }}</span>
</template>

<script>
export default {
    name: 'random-character-quote',
    props: {
        character: Object
    }
}
</script>

<style scoped />