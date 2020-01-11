<template>
  <div id="app">
    <VuePage :conf="pageConf"/>
  </div>
</template>

<script>
import VuePage from './components/VuePage.vue';

export default {
  data: function() {
    return {
      pageConf: {
        totalCount: 70,
        size: 10,
        showLen: 5,
        changeFn: this.pageChangeFn
      }
    }
  },
  components: {
    VuePage
  },
  methods: {
    pageChangeFn() {
      console.log(1111);
    }
  }
}
</script>

<style>

</style>
