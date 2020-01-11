<template>
    <div class="service">
        <div class="container">
            <ul>
                <li><span class="icon-setting1"></span>预约维修</li>
                <li><span class="icon-setting2"></span>7天无理由</li>
                <li><span class="icon-setting3"></span>15天免费退换</li>
                <li><span class="icon-setting4"></span>满150包邮</li>
            </ul>

        </div>
    </div>
</template>

<script>
    export default{
        name:'service-bar'
    }
</script>

<style lang="scss">
@import "../assets/scss/base";
@import "../assets/scss/mxin";
    .service{
        padding: 33px 0;
        color:#666666;
        font-size:16px;

        li{
            display: inline-block;
            width:24.9%;
            text-align: center;
            border-right: 1px solid #E5E5E5;
            span{
                display: inline-block;
                width: 20px;
                height: 20px;
                margin-right: 8px;
                vertical-align: middle;
            }
            .icon-setting1{
                @include bgImg(20px,20px,'/imgs/icon-setting.png')
            }
            .icon-setting2{
                @include bgImg(20px,20px,'/imgs/icon-7day.png')
            }
            .icon-setting3{
                @include bgImg(20px,20px,'/imgs/icon-15day.png')
            }
            .icon-setting4{
                @include bgImg(20px,20px,'/imgs/icon-post.png')
            }
        }


    }
</style>
