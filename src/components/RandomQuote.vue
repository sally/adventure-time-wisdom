<template>
    <span>{{ testMsg }}</span>
</template>

<script>
export default {
    name: 'random-quote',
    props: {
        testMsg: String
    }
}
</script>

<style scoped />