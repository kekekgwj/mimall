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
        <div class="ads">
          <a href="'/#/product/' + item.id" v-for="(item,index) in adsList" :key="index">
            <img :src="item.img" alt="">
          </a>
        </div>
        <div class="banner">
          <a href="/#/product/30">
            <img src="/imgs/banner-1.png" alt="">
          </a>
        </div>
      </div>
    <div class="product-box">
      <div class="container">
        <h2>手机</h2>
        <div class="wrapper">
          <div class="banner-left">
            <a href="/#/product/35"><img src="/imgs/mix-alpha.jpg"></a>
          </div>
          <div class="list-box">
            <div class="list" v-for="(arr,i) in phoneList" :key="i">
              <div class="item" v-for="(phone,index) in arr" :key="index">
                <span :class="{'new-pro':index%2 == 0,'kill-pro':index % 2==1 }">新品</span>
                <div class="item-img">
                  <img :src="phone.mainImage" alt="">
                </div>
                <div class="item-info">
                  <h2>{{phone.name}}</h2>
                  <p>{{phone.subtitle}}</p>
                  <p class="price">{{phone.price | currency()}}</p>
                </div>
              </div>
            </div>
          </div>
        </div>

      </div>


    </div>

    <ServiceBar></ServiceBar>
    <Model
            title="提示"
            sureText="查看购物车"
            btnType="1"
            model-type="middle"
            :showModel="showModel">
      <template v-slot:body>
        <p>商品添加成功!</p>
      </template>

    </Model>
  </div>
</template>
<script>
  import ServiceBar from './../components/ServiceBar'
  import {swiper,swiperSlide} from 'vue-awesome-swiper'
  import 'swiper/dist/css/swiper.css'
  import Model from './../components/Model'
  export default{
    name:'idx',
    components:{
      ServiceBar,
      swiper,
      swiperSlide,
      Model
    },
    filters:{
      currency(val){
        if(!val) return '0,00';
        return '￥'+ val+'元'
      }
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
        showModel:true,

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
        ],
        adsList:[
          {
            id:33,
            img:'/imgs/ads/ads-1.png'
          },{
            id:48,
            img:'/imgs/ads/ads-2.jpg'
          },{
            id:45,
            img:'/imgs/ads/ads-3.png'
          },{
            id:47,
            img:'/imgs/ads/ads-4.jpg'
          }
        ],
        phoneList:[
          [0,0,0,0],[0,0,0,0]
        ]
      }
    },
    mounted(){
      this.getPhoneList();
    },
    methods:{
      getPhoneList(){
        this.axios.get('/products',{
          params:{
            categoryId:100012,
            pageSize:14
          }
        }).then(res => {
          res.list = res.list.slice(6,14);
          this.phoneList[0] = res.list.slice(0,4);
          this.phoneList[1] = res.list.slice(4,8);
        })

      }

    }
  }
</script>
<style lang="scss">
  @import "../assets/scss/mxin";
  @import "../assets/scss/base";
  @import "../assets/scss/config";

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
      .ads{
        display: flex;
        justify-content: space-between;
        margin-top: 14px;
        margin-bottom: 31px;
        a{
          width: 296px;
          height: 167px;
        }
      }
      .banner{
        margin-bottom: 50px;
      }
    }
    .product-box{
      background-color: $colorJ;
      padding: 30px 0 50px 0;
      .wrapper{
        display: flex;
        .banner-left{
          margin-right: 16px;
          img{
            width:224px;
            height: 619px;
          }
        }
        .list-box{
          h2{
            font-size: $fontF;
            height: 21px;
            line-height: 21px;
            color:$colorB;
            margin-bottom: 10px;
          }
          .list{
            display: flex;
            justify-content: space-between;
            width:960px;
            margin-bottom: 14px;
            &:last-child{
              margin-bottom: 0;
            }
            .item{
              width: 236px;
              height: 302px;
              background-color: $colorG;
              text-align: center;
              span{
                display: inline-block;
                width:67px;
                height: 24px;
                font-size: 14px;
                line-height: 24px;
                color:#ffffff;
                &.new-pro{
                  background-color: #7ECF68;
                }
                &.kill-pro{
                  background-color: #E82626;
                }

              }
              .item-img{
                img{
                  width: 100%;
                  height: 195px;
                }
              }
              .item-info{
                h2{
                  font-size: $fontJ;
                  color:$colorB;
                  line-height:$fontJ;
                  font-weight: bold;
                }
                p{
                  color:$colorD;
                  font-size: $fontJ;
                  line-height: $fontJ;;
                  margin:0 auto 5px;
                }
                .price{
                  color:#F20A0A;
                  font-size:$fontJ;
                  font-weight: bold;
                  cursor:pointer;
                  &:after{
                    content: ' ';
                    @include bgImg(22px,22px,'/imgs/icon-cart-hover.png');
                    margin-left: 5px;

                  }
                }
              }

            }


          }
        }
      }


    }
  }

</style>
