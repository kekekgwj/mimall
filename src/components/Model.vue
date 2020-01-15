<template>
<div class="model" v-show="showModel">
    <div class="mask"></div>
    <div class="model-dialog">
        <div class="model-header">
            <span>标题</span>
            <a href="javascript:;" class="icon-close"></a>
        </div>
        <div class="model-body">
            <slot name="body"></slot>
        </div>
        <div class="model-footer">
            <a href="javascript:;" class="btn">确定</a>
            <a href="javascript:;" class="btn">取消</a>
        </div>

    </div>
</div>
</template>

<script>
    export default{
        name:'model',
        props:{
            showModel:{
                type:Boolean,
                default:true
            },
            modelType:{
                type:String,
                default:'form'
            },
            title:String,
            btnType:String,
            sureText:{
                type:String,
                default:'确定'
            },
            cancelText:{
                type:String,
                default:'取消'
            }
        }
    }

</script>

<style lang="scss">
    @import "../assets/scss/mxin";
    @import "../assets/scss/base";
    @import "../assets/scss/config";
</style>
