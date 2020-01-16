<template>
<div class="login">
    <div class="header">
        <a href="/#/index"><img src="/imgs/login-logo.png" alt=""></a>
    </div>
    <div class="wrapper">
        <div class="container">
            <div class="login-form">
                <div class="login-method">
                    <p class="loginWithAccount">账号登录</p>
                    <P class="loginWithScan">扫码登录</P>
                </div>
                <div class="inputArea">
                    <input type="text" name="account"  class="account" placeholder="邮箱/手机号码/小米ID" v-model="username">
                    <input type="password" name="passwordInput" placeholder="密码" v-model="password">
                </div>

                <a href="javascript:;" class="btn" @click="login">登录</a>

                <div class="tips">
                    <div class="sms" @click="register">手机短信登录/注册</div>
                    <div class="reg">立即注册<span>|</span>忘记密码？</div>
                </div>
            </div>
        </div>
    </div>
    <div class="footer">
        <div class="footer-link">
            <p> made by weijie GUo</p>
        </div>
        <p class="copyright">Copyright ©2019 mi.futurefe.com All Rights Reserved.</p>
    </div>
</div>

</template>

<script>
    export  default {
        name: 'login',
        data(){
            return{
                username:'',
                password:'',
                userId:'',
                res:{}
            }
        },
        methods:{
            login(){
                let { username,password} = this;
                this.axios.post('/user/login',{
                    username,
                    password
                }).then((res)=>{
                    this.$cookie.set('userId',res.id,{expires:'10M'});
                    this.$store.dispatch('saveUserName',res.username);
                    alert('登录成功');
                    this.$router.push('/index')
                })
            },
            register(){
                this.axios.post('/user/register',{
                    username:'admin',
                    password:"admin",
                    email:'admin@163.com'
                }).then(()=>{
                   alert('注册成功')
                })

            }
        }
    }
</script>
<style lang="scss">
    @import '../assets/scss/model.scss';
    @import '../assets/scss/mxin.scss';
    @import '../assets/scss/config.scss';
    .login{
        .header{
            height: 112px;
            width:1226px;
            margin-right:auto;
            margin-left:auto;
            a{
                display: inline-block;
                margin-left: 391px;
            }
            img{
                width: auto;
                height: 100%;
            }



        }
        .wrapper{

            background:url('/imgs/login-bg.jpg') no-repeat center;
            .container{
                height: 576px;
                .login-form{
                    position: absolute;
                    right:20px;
                    bottom: 29px;
                    background-color: #ffffff;
                    height: 510px;
                    width: 410px;
                    box-sizing:border-box;
                    padding-left: 31px;
                    padding-right: 31px;
                    .login-method{
                        display: flex;
                        justify-content: center;
                        width: 348px;
                        margin-top:40px;
                        margin-bottom:49px;
                        p{
                            color:#666666;
                            font-size: 24px;
                            width: 97px;
                            height: 23px;
                            line-height: 23px;
                            &:hover{
                                color: #FF6600;
                            }
                        }
                        .loginWithAccount{
                            margin-right: 40px;
                            &:after{
                                content: '';
                                border-right: 2px solid $colorF;
                                height: 25px ;
                                margin-left: 20px;
                            }

                        }
                    }
                    .inputArea{
                        input{
                            outline: none;
                            border: 1px solid #E5E5E5;
                            width:100%;
                            height: 50px;
                            display: block;
                            font-size: 14px;
                            line-height:50px;
                            text-indent: 18px;
                        }
                        .account{
                            margin-bottom: 20px;
                        }
                    }
                    .btn{
                        width: 100%;
                        line-height: 50px;
                        margin-top:20px;
                        font-size:16px;
                    }
                    .tips{
                        margin-top:14px;
                        display:flex;
                        justify-content:space-between;
                        font-size:14px;
                        cursor:pointer;
                        .sms{
                            color:#FF6600;
                        }
                        .reg{
                            color:#999999;
                            span{
                                margin:0 7px;
                            }
                        }
                    }
                }

            }
        }
        .footer{
            height:100px;
            padding-top:60px;
            color:#999999;
            font-size:16px;
            text-align:center;
            .footer-link{
                a{
                    color:#999999;
                    display:inline-block;
                }
                span{
                    margin:0 10px;
                }
            }
            .copyright{
                margin-top:13px;
            }
        }


    }

</style>
