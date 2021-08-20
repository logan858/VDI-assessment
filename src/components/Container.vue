<template>
    <div class="container">
        <Categories/>
    </div>
</template>

<script>
    import Categories from './Categories.vue'
    export default {
        name: 'Container',
        components: { Categories },
    }
</script>


<style scoped>
    .container {
        height: 75vh;
        width: 75vw;
        background: rgba(71, 71, 71, 0.1);
        border-radius: 2px;
        padding: 20px;
        margin: 10px;
        box-shadow: 0 0 1px 1px rgba(0, 0, 0, 0.3);
    }
</style>