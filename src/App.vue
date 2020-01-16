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
  },
  methods:{
    getUser(){
      this.axios.get('/user').then((res)=>{
          this.$store.dispatch('saveUserName',res.username);
      })

    },
    getCartCount(){
      this.axios.get('/carts/products/sum').then((res)=>{
        this.$store.dispatch('saveCartCount',res);
      })

    }
  },
  mounted() {
    this.getUser();
    this.getCartCount();
  }

}
</script>

<style lang="scss">
@import './assets/scss/reset.scss';
@import './assets/scss/model.scss';
@import './assets/scss/mxin.scss';
@import './assets/scss/config.scss';
</style>
