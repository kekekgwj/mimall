<template>
  <div class="header">
    <div class="nav-topbar">
      <div class="container">
        <div class="topbar-menu">
          <a href="javascript:;">小米商城</a>
          <a href="javascript:;">MUI</a>
          <a href="javascript:;">云服务</a>
          <a href="javascript:;">协议规则</a>
        </div>
        <div class="topbar-user">
          <a href="javascript:;" v-if="username">{{username}}</a>
          <a href="javascript:;" v-if="!username" @click="goToLogin">登录</a>
          <a href="javascript:;" v-if="username">我的订单</a>
          <a href="javascript:;" class="my-cart" @click="goToCart()"><span class="icon-cart"></span>购物车({{cartCount}}})</a>
        </div>
      </div>
    </div>
    <div class="nav-header">
      <div class="container">
        <div class="header-logo">
          <a href="/#/index"></a>
        </div>
        <div class="header-menu">
          <div class="item-menu">
            <span>小米手机</span>
            <div class="children">
              <ul>
                <li class="product" v-for="(item,index) in phoneList" :key="index">
                  <a :href="'/#/product'+item.id" target="_blank">
                      <div class="pro-img">
                        <img :src="item.mainImage"></div>
                      <div class="pro-name" v-text="item.name"></div>
                      <div class="pro-price" >{{item.price | currency}}</div>
                  </a>
                </li>
              </ul>
            </div>
          </div>
          <div class="item-menu">
            <span>RedMi</span>
            <div class="children">
              <ul>
                <li class="product" v-for="(item,index) in phoneList" :key="index">
                  <a :href="'/#/product'+item.id" target="_blank">
                    <div class="pro-img">
                      <img :src="item.mainImage"></div>
                    <div class="pro-name" v-text="item.name"></div>
                    <div class="pro-price" >{{item.price | currency}}</div>
                  </a>
                </li>
              </ul>
            </div>
            <div class="children"></div>
          </div>
          <div class="item-menu">
            <span>电视</span>
            <div class="children">
              <ul>
                <li class="product">
                  <a href="" target="_blank">
                    <div class="pro-img"><img src="/imgs/nav-img/nav-3-1.jpg"></div>
                    <div class="pro-name">小米C9 Pr0</div>
                    <div class="pro-price">2599</div>
                  </a>
                </li>
                <li class="product">
                  <a href="" target="_blank">
                    <div class="pro-img"><img src="/imgs/nav-img/nav-3-2.jpg"></div>
                    <div class="pro-name">小米C9 Pr0</div>
                    <div class="pro-price">2599</div>
                  </a>
                </li>
                <li class="product">
                  <a href="" target="_blank">
                    <div class="pro-img"><img src="/imgs/nav-img/nav-3-3.png"></div>
                    <div class="pro-name">小米C9 Pr0</div>
                    <div class="pro-price">2599</div>
                  </a>
                </li>
                <li class="product">
                  <a href="" target="_blank">
                    <div class="pro-img"><img src="/imgs/nav-img/nav-3-4.jpg"></div>
                    <div class="pro-name">小米C9 Pr0</div>
                    <div class="pro-price">2599</div>
                  </a>
                </li>
                <li class="product">
                  <a href="" target="_blank">
                    <div class="pro-img"><img src="/imgs/nav-img/nav-3-5.jpg"></div>
                    <div class="pro-name">小米C9 Pr0</div>
                    <div class="pro-price">2599</div>
                  </a>
                </li>
                <li class="product">
                  <a href="" target="_blank">
                    <div class="pro-img"><img src="/imgs/nav-img/nav-3-6.png"></div>
                    <div class="pro-name">小米C9 Pr0</div>
                    <div class="pro-price">2599</div>
                  </a>
                </li>
              </ul>
            </div>
          </div>
        </div>
        <div class="header-search">
          <div class="wrapper">
            <input type="text" name="keyword">
            <a href="javascript:;"></a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
  export default{
    name:'nav-header',
    data(){
      return{
        phoneList:[]
      }
    },
    computed:{
      username:function(){
        return this.$store.state.username;
      },
      cartCount:function(){
        return this.$store.state.cartCount;
      }
    },
    filters:{
      currency(val){
        if(!val) return '0,00';
        return '￥'+ val+'元'
      }
    },
    mounted(){
      this.getProductList();

    },
    methods:{
      getProductList(){
        this.axios.get('/products',{
          params:{
            categoryId:'100012',
          }
        }).then((res)=>{
            this.phoneList = res.list.slice(0,6);
        })
      },
      goToCart(){
        this.$router.push('/cart')
      },
      goToLogin(){
        this.$router.push('/login')
      }
    }
  }
</script>
<style lang="scss">
  @import '../assets/scss/base.scss';
  @import '../assets/scss/mxin.scss';
  @import '../assets/scss/config.scss';

  .header{
    .nav-topbar{
      height:39px;
      line-height:39px;
      background-color:#333333;
      color:#B0B0B0;
      .container{
        @include flex();
        a{
          display:inline-block;
          color:#B0B0B0;
          margin-right:17px;
        }
        .my-cart{
          width:110px;
          background-color:#FF6600;
          text-align:center;
          color:#ffffff;
          .icon-cart{
            display:inline-block;
            width:16px;
            height:12px;
            background:url('/imgs/icon-cart-checked.png') no-repeat center;
            background-size:contain;
            margin-right:4px;
          }
        }
      }
    }
    .nav-header{
      .container{
        position: relative;
        height: 112px;
        display: flex;
        justify-content: space-between;
        align-items: center;
        .header-logo{
          display:inline-block;
          width: 55px;
          height: 55px;
          background-color: #FF6600;
          a{
            display: inline-block;
            width: 110px;
            height: 55px;
            &:before{
              content:'';
              @include bgImg(55px,55px,'/imgs/mi-logo.png',55px);
              transition: .2s;
            }
            &:after{
              content:'';
              @include bgImg(55px,55px,'/imgs/mi-home.png',55px);
              transition: .2s;

            }
            &:hover:before{
              margin-left: -55px;
              transition:margin .2s;
            }
          }
        }
        .header-menu{
          display: inline-block;
          padding-left: 209px;
          width:643px;
          .item-menu{
            display: inline-block;
            color: #333333;
            font-weight: bold;
            font-size: 16px;
            margin-left:30px;
            line-height: 112px;
            span{
              cursor:pointer;
            }
            &:hover{
              color:$colorA;
              .children{
                height: 220px;
                opacity: 1;
              }
            }
            .children{
              position: absolute;
              top:112px;
              left:0;
              width:1226px;
              height: 0;
              opacity: 0;
              overflow: hidden;
              border-top: 1px solid #e5e5e5;
              box-shadow:0px 7px 6px 0px rgba(0, 0, 0, 0.11);
              background-color: #ffffff;
              transition: height .5s;
              .product{
                position: relative;
                float:left;
                width:16.6%;
                height: 220px;
                font-size:12px;
                line-height: 12px;
                text-align: center;
                z-index: 10;
                background-color: #ffffff;
                a{
                  display: inline-block;
                }
                img{
                  height: 111px;
                  width:auto;
                  margin-top: 26px;
                }
                .pro-img{
                  height:137px
                }
                .pro-name{
                  font-weight: bold;
                  margin-top: 19px;
                  margin-bottom: 8px;
                  color:$colorB;
                }
                .pro-price{
                  color:$colorA;
                }
                &:after{
                  content:' ';
                  position:absolute;
                  top:28px;
                  right:0;
                  border-left: 1px solid $colorF;
                  height: 100px;
                  width: 1px;
                }
                &:last-child:after{
                  display: none;
                }
              }
            }
          }

        }
        .header-search{
          width:319px;
          .wrapper{
            height: 50px;
            border:1px solid #E0E0E0;
            display: flex;
            align-items: center;
            input{
              border : none;
              border-right: 1px solid #E0E0E0;
              width:264px;
              height: 50px;
              padding-left: 13px;
            }
            a{
              display: inline-block;
              width: 18px;
              height:18px;
              background:url('/imgs/icon-search.png') no-repeat center;
              background-size: contain;
              margin-left: 12px;
            }
          }
        }
      }
    }
  }
</style>
