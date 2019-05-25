<template>

  <div id="app">
    <app-head></app-head>


    <app-body></app-body>


    <app-footer></app-footer>
  </div>


</template>

<script>
import Header from './components/Header.vue'
import Body from './components/Body.vue'
import Footer from './components/Footer.vue'

export default {
  components: {
    appHead: Header,
    appBody: Body,
    appFooter: Footer,
  },
}
</script>

<style>

</style>
