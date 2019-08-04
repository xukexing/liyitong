<template>
    <div class="nav-warp">
        <div class="header">
            <div class="nav" v-if="info!==null">
            <h1><img :src="info.logo" alt=""></h1>
            <ul class="parent-menu">
                <li class="parent-item" v-for="(item,index) in info.navList" :key="index">
                    <span v-text="item.name"></span>
                    <ul class="child-menu" v-if="item.child.length>0">
                        <li class="child-title" v-text="item.name"></li>
                        <li class="child-item" v-for="(val,index) in item.child" :key="index">
                            <router-link :to="val.url" v-text="val.name"></router-link>
                        </li>
                    </ul>
                </li>
            </ul>
            <div class="btns">
                <button><router-link to="logo">登录</router-link></button>
                <button>
                    <span v-text="info.sales.name" @click="salesChange"></span>
                    <div class="sales-click" :class="{'sales-show': salesClick}">
                        <div class="connect"></div>
                        <h3 @click="salesChange">X</h3>
                        <ul class="alret">
                            <li class="alret-item" v-for="(item,index) in info.sales.click" :key="index">
                                <span>ic</span>
                                <div class="phone">
                                    <h2 v-text="item.name"></h2>
                                    <p v-text="item.number"></p>
                                </div>
                            </li>
                        </ul>
                    </div>
                </button>
            </div>
        </div>
        </div>
        
    </div>
</template>

<script>
import axios from 'axios'
export default {
    data() {
        return {
            //header所有数据
            info:null,
            //判断是否显示联系销售的信息
            salesClick:false
        }
    },
    mounted() {
        // axios.get(' https://www.easy-mock.com/mock/5d26e68c549bcc6acf1d3e66/example/nav1')
         axios.get('../../.././static/header.json')
                .then(res=>{
                    // console.log(res.data.data); 
                    this.info= res.data.data
                }).catch(err=>{
                    console.log(err);
                })
    },
    methods: {
        //点击联系销售 显示与隐藏联系信息
        salesChange(){
            // console.log(this.salesClick)
            this.salesClick=!this.salesClick
        }
    },
}
</script>
<style lang="stylus" scoped>
@import '../.././assets/stylus/variable.styl'
.nav-warp
    height 88px
    width 100%
    background #fff 
    position fixed
    top 0
    left 0
    z-index 100
    .header
        margin 0 110px
        .nav
            height 88px
            width 100%
            background pink
            display flex
            align-items center
            justify-content space-between
            h1
                width 131px 
                height 47px
                cursor pointer
                img 
                    width 131px
                    height 100%
            .parent-menu
                width 68%
                height 100%
                text-align right 
                box-sizing border-box
                .parent-item
                    line-height 88px
                    text-align center
                    padding 0 40px
                    display inline-block
                    font-size $font-size-xl
                    position relative
                    .child-menu
                        position absolute
                        top 0
                        left 0
                        width 100%
                        font-size $font-size-l
                        text-align cente
                        padding 35px 0 20px
                        display none
                        background $background-opt
                        .child-title
                            line-height 18px
                            margin-bottom 10px
                            font-size $font-size-xl
                        .child-item
                            line-height 40px
                            display block
                            a
                                color $color-text
                                display block
                            a:hover
                                color $theme-color
                .parent-item:hover
                    background $background-opt
                .parent-item:hover .child-menu
                    display block
            .btns
                height 100%
                display flex
                align-items center
                button
                    display block
                    text-align center
                    line-height 40px
                    width 120px
                    font-size $font-size-xl
                    border-radius: 6px
                    margin-left 20px
                    background $background-opt
                    color $color-text
                button:nth-of-type(2)
                    background $theme-color
                    position relative
                .sales-click
                    display none
                    position absolute
                    top 80px
                    left 0 
                    right 0
                    margin-left -180px
                    box-shadow: 0 -5px 10px 0 rgba(0,0,0,.1); 
                    background #ffffff
                    color #000
                    width 360px
                    padding 0 30px 20px
                    box-sizing border-box
                    &.sales-show
                        display block
                    .connect
                        position absolute
                        top -20px
                        right 80px
                        width 40px
                        height 40px
                        transform rotate(45deg)
                        background red
                        background #ffffff
                        box-shadow: 0 -5px 10px 0 rgba(0,0,0,.1);
                    h3
                        text-align right
                    .alret
                        width 100%
                        .alret-item
                            display flex
                            span
                                font-size 50px
                                line-height 60px
                            .phone
                                height 60px
                                display flex
                                flex-direction column
                                justify-content center
                                text-align left 
                                box-sizing border-box
                                padding-left 20px
                                h2,p
                                    color $color-text-s 
                                    font-size $font-size-l
                                    line-height $font-size-l
                                p
                                    color $theme-color
                                    margin-top 10px
                
</style>

