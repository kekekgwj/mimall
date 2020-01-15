<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: 'app',
  components: {

  },
  data(){

    return {
      a:{}
    }
  }

}
</script>

<style lang="scss">
@import './assets/scss/reset.scss';
@import './assets/scss/model.scss';
@import './assets/scss/mxin.scss';
@import './assets/scss/config.scss';
</style>
