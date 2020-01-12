<template>
  <div class="index">
      <div class="container">
        <div class="swiper-box">
          <div class="nav-menu">
            <ul>
              <li class="menu-item">
                <a href="javascript:;">手机  电话卡</a>
                <div class="children">
                  <ul v-for="(item,index) in menuList" :key="index">
                    <li v-for="(sub,index) in item" :key="index">
                    <a :href="'/#/product/'+ (sub? sub.id:'')">
                      <img :src="sub?sub.img : '/imgs/item-box-1.png'" alt="">
                      {{sub?sub.name:'小米9'}}

                    </a>
                    </li>
                  </ul>

                </div>
              </li>
              <li class="menu-item">
                <a href="javascript:;">配件</a>
                <div class="children"></div>
              </li>
              <li class="menu-item">
                <a href="javascript:;">电视  黑子 </a>
                <div class="children"></div>
              </li>
              <li class="menu-item">
                <a href="javascript:;">家电  插线板</a>
                <div class="children"></div>
              </li>
              <li class="menu-item">
                <a href="javascript:;">出行  穿戴</a>
                <div class="children"></div>
              </li>
              <li class="menu-item">
                <a href="javascript:;">智能  路由器</a>
                <div class="children"></div>
              </li>
              <li class="menu-item">
                <a href="javascript:;">电源</a>
                <div class="children"></div>
              </li>
              <li class="menu-item">
                <a href="javascript:;">小米生活</a>
                <div class="children"></div>
              </li>
            </ul>
          </div>
          <swiper :options="swiperOption">
            <swiper-slide v-for="(item,index) in slideList" :key="index">
              <a :href="'/#/product'+item.id"><img :src="item.img" alt="11111"></a>
            </swiper-slide>
            <div class="swiper-pagination"  slot="pagination"></div>
            <div class="swiper-button-prev" slot="button-prev"></div>
            <div class="swiper-button-next" slot="button-next"></div>
          </swiper>
        </div>
        <div class="ads"></div>
        <div class="banner"></div>
        <div class="product-box"></div>
      </div>
    <ServiceBar></ServiceBar>
  </div>
</template>
<script>
  import ServiceBar from './../components/ServiceBar'
  import {swiper,swiperSlide} from 'vue-awesome-swiper'
  import 'swiper/dist/css/swiper.css'
  export default{
    name:'idx',
    components:{
      ServiceBar,
      swiper,
      swiperSlide
    },
    data(){
      return{
        swiperOption:{
          autoplay:true,
          loop:true,
          effect : 'cube',
          cubeEffect: {
            slideShadows: true,
            shadow: true,
            shadowOffset: 100,
            shadowScale: 0.6
          },
          pagination:{
            el: '.swiper-pagination',
            clickable:true
          },
          navigation: {
            nextEl: '.swiper-button-next',
            prevEl: '.swiper-button-prev',
          }
        },

        slideList:[
          {
            id:'42',
            img:'/imgs/slider/slide-1.jpg'
          },
          {
            id:'45',
            img:'/imgs/slider/slide-2.jpg'
          },
          {
            id:'46',
            img:'/imgs/slider/slide-3.jpg'
          },
          {
            id:'',
            img:'/imgs/slider/slide-4.jpg'
          },
          {
            id:'',
            img:'/imgs/slider/slide-5.jpg'
          }
        ],
        menuList:[
          [
            {
              id:30,
              img:'/imgs/item-box-1.png',
              name:'小米CC9'
            },
            {
              id:31,
              img:'/imgs/item-box-2.png',
              name:'小米8青春版'
            },
            {
              id:32,
              img:'/imgs/item-box-3.jpg',
              name:'小米8旗舰版'
            },
            {
              id:33,
              img:'/imgs/item-box-4.jpg',
              name:'移动4G专区'
            }
          ],
          [0,0,0,0],[0,0,0,0],[0,0,0,0],[0,0,0,0]
        ]

      }
    }
  }
</script>
<style lang="scss">
  @import "../assets/scss/mxin";
  .index{
    .container{
      .nav-menu{
        box-sizing:border-box;
        position: absolute;
        width:264px;
        height:451px;
        z-index:9;
        padding:26px 0;
        background-color: #55585A7a;
        .menu-item{
          position: relative;
          height: 50px;
          line-height: 50px;
          a{
            font-size:16px;
            color:#ffffff;
            padding-left: 30px;
            &:after{
              position: absolute;
              right: 30px;
              top:17.5px;
              content: ' ';
              @include bgImg(10px,15px,'/imgs/icon-arrow.png')

            }
          }
          &:hover{
            background-color: #FF6600;
            .children{
              display: block;
            }
          }
          .children{
            display: none;
            position: absolute;
            width:962px;
            height: 451px;
            background-color: #ffffff;
            top:0;
            left: 264px;
            border: 1px solid #e5e5e5;
            ul{
              display: flex;
              justify-content: space-between;
              height: 75px;
              margin-bottom: 20px;
              li{
                height: 75px;
                line-height: 75px;
                flex:1;
                padding-left: 23px;
              }
              img{
                width:42px;
                height: 35px;
                vertical-align: middle;
                margin-right: 15px;
              }
              a{
                color:#000000;
                font-size: 14px;
              }
            }

          }
        }
      }
      .swiper-box{
        .swiper-container{
          height: 451px;
          .swiper-button-prev{
            left:274px
          }
          img{
            width: 100%;
            height: 100%;
          }
        }
      }
    }
  }

</style>
