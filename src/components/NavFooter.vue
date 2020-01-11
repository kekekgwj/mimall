<template>
  <div class="footer">
    <div class="footer-logo">
      <div class="logo"></div>
      <p class="brand">小米商城</p>
    </div>
    <div class="footer-link">
      <div class="copyRight">This is made by <span class="domin">Weijie Guo</span></div>
  </div>
  </div>
</template>
<script>
  export default{
    name:'nav-footer'
  }
</script>
<style lang="scss">
  @import "../assets/scss/mxin";
  .footer{
    position: absolute;
    bottom: 0;
    height: 234px;
    width:100%;
    border-top:4px solid #FF6600;
    background:#333333;
    font-size:16px;
    text-align: center;
    .footer-logo{
      height: 65px;
      width: 64px;
      margin:46px auto 0;
      .logo{
        @include bgImg(53px,36px,'/imgs/logo-mi.png');
        padding: 0 3px 13px 8px
      }
      .brand{
        color:#999999
      }
    }
    .footer-link{
      margin-top: 31px;
      .copyRight{
        color:#999999;
        .domin{
          color:#FF6600;
        }

      }

    }
  }
</style>
