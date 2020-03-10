<template>
    <div class="index">
        <div class="container">
            <div class="swiper-box">
                <div class="nav-menu">
                    <ul class="menu-wrap">
                        <li class="menu-item">
                            <a href="javascript:;">手机 电话卡</a>
                            <div class="children">
                                <ul v-for="item in menuList" :key="item.id"> 
                                    <li v-for="(sub,index) in item" :key="index">
                                        <a :href="sub.id?'/#/product/'+sub.id:''">
                                            <img :src="sub?sub.img:'/imgs/item-box-1.png'" alt="">
                                            {{sub?sub.name:'小米9'}}
                                        </a>
                                    </li>
                                </ul>
                            </div>
                        </li>
                        <li class="menu-item">
                            <a href="javascript:;">电视 盒子</a>
                            <div class="children"></div>
                        </li>
                        <li class="menu-item">
                            <a href="javascript:;">笔记本 平板</a>
                            <div class="children"></div>
                        </li>
                        <li class="menu-item">
                            <a href="javascript:;">家电 插线板</a>
                            <div class="children"></div>
                        </li>
                        <li class="menu-item">
                            <a href="javascript:;">出行 穿戴</a>
                            <div class="children"></div>
                        </li>
                        <li class="menu-item">
                            <a href="javascript:;">智能 路由器</a>
                            <div class="children"></div>
                        </li>
                        <li class="menu-item">
                            <a href="javascript:;">电源 配件</a>
                            <div class="children"></div>
                        </li>
                        <li class="menu-item">
                            <a href="javascript:;">生活 箱包</a>
                            <div class="children"></div>
                        </li>
                    </ul>
                </div>
                <swiper :options="swiperOption">
                    <swiper-slide v-for="(item,index) in slideList" :key="index">
                        <a :href="'/#/product/'+item.id">
                            <img :src="item.img" >
                        </a>
                    </swiper-slide>
                    <div class="swiper-pagination"></div>
                    <!-- Optional controls -->
                    <div class="swiper-pagination"  slot="pagination"></div>
                    <div class="swiper-button-prev" slot="button-prev"></div>
                    <div class="swiper-button-next" slot="button-next"></div>
                </swiper>
            </div>
            <div class="ads-box">
                <a :href="'/#/product/'+item.id" v-for="(item,index) in adsList" :key="index">
                    <img v-lazy="item.img" alt="">
                </a>
            </div>
            <div class="banner">
                <a href="/#/product/30" >
                    <img v-lazy="'/imgs/banner-1.png'" alt="">
                </a>
            </div>     
        </div>
        <div class="product-box">
            <div class="container">
                <h2>手机</h2>
                <div class="wrapper">
                    <div class="banner-left">
                        <a href="/#/product/35">
                            <img v-lazy="'/imgs/mix-alpha.jpg'" alt="">
                        </a>
                    </div>
                    <div class="list-box">
                        <div class="list" v-for="(arr,i) in phoneList" :key="i">
                            <div class="item" v-for="(item,j) in arr" :key="j">
                                <span :class="{'new-pro':j%2==0}">新品</span>
                                <div class="item-img">
                                    <img v-lazy="item.mainImage" >
                                </div>
                                <div class="item-info">
                                    <h3>{{item.name}}</h3>
                                    <p>{{item.subtitle}}</p>
                                    <p class="price" @click="addCart(item.id)">{{item.price | currency}}</p>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <service-bar/>
        <modal title="提示" sureText="查看购物车详情" btnType="1" modalType="middle" :showModal="showModal" @submit="goToCart" @cancel="showModal=false">
            <template v-slot:body>
                <p>商品添加成功！</p>
            </template>
        </modal>
    </div>
</template>
<script>
import ServiceBar from '../components/ServiceBar'
import Modal from '../components/Modal'
import 'swiper/dist/css/swiper.css'
import { swiper, swiperSlide } from 'vue-awesome-swiper'
export default {
    name:'index',
    components:{
        ServiceBar,
        swiper,
        swiperSlide,
        Modal
    },
    data(){
        return{
            swiperOption:{
                autoplay:true,
                loop:true,
                effect:'cube',
                cubeEffect: {
                    shadowOffset: 100,
                    shadowScale: 0.6
                },
                pagination: {
                    el: '.swiper-pagination',
                    clickable :true,
                },
                navigation: {
                nextEl: '.swiper-button-next',
                prevEl: '.swiper-button-prev'
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
                        id:'30',
                        img:'/imgs/item-box-1.png',
                        name:'小米CC9'
                    },
                    {
                        id:'31',
                        img:'/imgs/item-box-2.png',
                        name:'小米8青春版'
                    },
                    {
                        id:'32',
                        img:'/imgs/item-box-3.jpg',
                        name:'Redmi K20 Pro'
                    },
                    {
                        id:'33',
                        img:'/imgs/item-box-4.jpg',
                        name:'移动4G专区'
                    }
                ],[0,0,0,0],[0,0,0,0],[0,0,0,0],[0,0,0,0],[0,0,0,0]
            ],
            adsList:[
                {
                    id:33,
                    img:'/imgs/ads/ads-1.png'
                },
                {
                    id:45,
                    img:'/imgs/ads/ads-2.jpg'
                },
                {
                    id:47,
                    img:'/imgs/ads/ads-3.png'
                },
                {
                    id:48,
                    img:'/imgs/ads/ads-4.jpg'
                }
            ],
            phoneList:[],
            showModal:false
        }
    },
    mounted(){
        this.init();
    },
    filters:{
        currency(val){
            if(!val) return '0.00';
            return '¥'+val.toFixed(2)+'元';
        }   
    },
    methods:{
        init(){
            this.axios.get('/products',{
                params:{
                    categoryId:100012,
                    pageSize:14
                }
            }).then((res)=>{
                res.list = res.list.slice(6,14);
                this.phoneList = [res.list.slice(0,4),res.list.slice(4,8)]
            })
        },
        addCart(id){
            this.axios.post('/carts',{
                productId:id,
                selected:true
            }).then((res)=>{
                this.showModal = true;
                this.$store.dispatch('saveCartCount',res.cartTotalQuantity);
            }).catch(()=>{
                this.showModal = true;
            })
        },
        goToCart(){
            this.$router.push('/cart');
        }
    }
}
</script>
<style lang="scss">
@import "../assets/scss/base.scss";
@import "../assets/scss/mixin.scss";
@import "../assets/scss/config.scss";
.index{
    .swiper-box{
        .swiper-container{
            height: 451px;
            .swiper-button-prev{
                left:274px;
            }
            img{
                width:100%;
                height: 100%;
            }
        }
        .nav-menu{
            position:absolute;
            z-index: 8;
            height: 451px;
            width:264px;
            background:#55585a7a;
            padding:26px 0px;
            box-sizing: border-box;
            .menu-wrap{
                .menu-item{
                    height: 50px;
                    line-height: 50px;
                    >a{
                        display: block;
                        height: 50px;
                        width:233px;
                        color: $colorG;
                        font-size: $fontI;
                        padding-left: 30px;
                        background:url(/imgs/icon-arrow.png)no-repeat 233px center;
                        background-size:10px 15px;           
                    }                
                    .children{
                        display:none;
                        width:962px;
                        height:451px;
                        position:absolute;
                        left:264px;
                        top:0px;
                        background:$colorG;
                        ul{
                            display:flex;
                            justify-content: space-between;
                            height: 75px;
                            li{
                                height: 75px;
                                line-height: 75px;
                                flex:1;
                                padding-left:23px;
                                img{
                                    width:42px;
                                    height:35px;
                                    vertical-align: middle;
                                    margin-right: 15px;
                                }
                                a{
                                    color:$colorB;
                                    font-size: $fontJ;
                                }
                            }
                            
                        }
                    }
                    &:hover{
                        background:$colorA;
                        .children{
                            display:block;
                        }
                    }
                }           
            }
        }
    }
    .ads-box{
        @include flex();
        margin:14px 0 30px 0;
        a{
            width:296px;
            height: 167px;
        }
    }
    .banner{
        margin-bottom: 50px;
    }
    .product-box{
        background:$colorJ;       
            h2{
                line-height: 70px;
                height: 70px;
                color:$colorB;
                font-size:$fontF;
            }
            .wrapper{
                display:flex;
                .banner-left{
                    margin-right: 16px;
                    img{
                        width: 224px;
                        height: 619px;
                    }
                }
                .list-box{
                    .list{
                        width:986px;
                        @include flex();
                        margin-bottom:14px;
                        &:last-child{
                            margin:0;
                        }
                        .item{
                            width:236px;
                            height:302px;
                            background:$colorG;
                            text-align: center;
                            span{
                                display: inline-block;
                                width:67px;
                                height: 24px;
                                line-height:24px;
                                color:$colorG;
                                font-size:$fontJ;
                                &.new-pro{
                                    background:#7ECF68
                                }
                                &.kill-pro{
                                    background:#E82626;
                                }
                            }
                            .item-img{

                                img{
                                    height: 195px;
                                    width:100%;
                                }
                            }
                            .item-info{
                                h3{
                                    font-size:$fontJ;
                                    color:$colorB;
                                    line-height:14px;
                                    font-weight: bold;
                                }
                                p{
                                    color:$colorD;
                                    line-height:14px;
                                    margin:6px auto 13px auto;
                                }
                                .price{
                                    color:#F20A0A;
                                    font-size:$fontJ;
                                    font-weight: bold;
                                    cursor: pointer;
                                    &:after{
                                        content: "";
                                        @include bgImg(22px,22px,'/imgs/icon-cart-hover.png');
                                        margin-left:5px;
                                        vertical-align: middle;
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