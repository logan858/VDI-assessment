<template>
    <div id="app">
      <Container/>
    </div>
</template>

<script>
    import Container from './components/Container.vue'

    export default {
      components: { Container },
      name: 'App',
      // data() {
      //   return {
      //     category: "test",
      //     documents: "docu-tests",
      //     counter: 0
      //   }
      // },
      // computed: {
      //   bothStates() {
      //     return `${this.category} ${this.documents}`
      //   }
      // },
      // methods: {
      //   countCounter() {
      //     this.counter++
      //   }
      // }
    }
</script>



<style>
    #app {
      font-family: Avenir, Helvetica, Arial, sans-serif;
      -webkit-font-smoothing: antialiased;
      -moz-osx-font-smoothing: grayscale;
      text-align: center;
      display: flex;
      height: 90vh;
      justify-content: center;
      align-items: center;
    }
</style>
