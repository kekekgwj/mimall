<template>
    <transition name="slide">
        <div class="model" v-show="showModel">
            <div class="mask"></div>
            <div class="model-dialog">
                <div class="model-header">
                    <span>{{title}}</span>
                    <a href="javascript:;" class="icon-close" @click="closeDia"></a>
                </div>
                <div class="model-body">
                    <slot name="body"></slot>
                </div>
                <div class="model-footer">
                    <a href="javascript:;" class="btn" v-if="btnType == 1" @click="$emit('submit')" v-text="sureText"></a>
                    <a href="javascript:;" class="btn" v-if="btnType == 2" @click="$emit('cancel')">取消</a>
                    <div class="btn-group" v-if="btnType == 3">
                        <a href="javascript:;" class="btn"  @click="$emit('submit')" v-text="sureText">确定</a>
                        <a href="javascript:;" class="btn btn-default" @click="$emit('cancel')">取消</a>
                    </div>

                </div>

            </div>
        </div>
    </transition>

</template>

<script>
    export default{
        name:'model',
        methods:{
            closeDia(){
                this.showModel = !this.showModel;
            }
        },
        props:{
            showModel:{
                type:Boolean,
                default:false
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
    @import "../assets/scss/button";
</style>
