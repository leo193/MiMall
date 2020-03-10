<template>
    <div class="ali-pay">
        <order-header title="支付宝支付">
            <template v-slot:tips>
                <span>请谨防钓鱼链接或诈骗电话，了解更多</span>
            </template>
        </order-header>
        <loading v-if="loading"></loading>
        <div class="form" v-html="content"></div>
    </div>
</template>
<script>
import Loading from '../components/Loading.vue'
import OrderHeader from '../components/OrderHeader'
export default {
   name:'alipay',
   components: {
       Loading,
       OrderHeader
   },
   data() {
       return{
           orderId:this.$route.query.orderId,
           content:'',
           loading:true
       }
   },
   mounted() {
       this.paySubmit();
   },
   methods:{
       paySubmit(){
           this.axios.post('/pay',{
                orderId:this.orderId,
                orderName:'Vue高仿小米商城', //扫码支付时订单名称
                amount:0.01, //单位元
                payType:1
           }).then((res)=>{
               this.content=res.content;
               setTimeout(()=>{
                   document.forms[0].submit()
               },100)
           })
       }
   }
}
</script>