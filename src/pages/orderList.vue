<template>
  <div class="order-list">
    <order-header title="订单列表">
      <template v-slot:tips>
        <span>请谨防钓鱼链接或诈骗电话，了解更多</span>
      </template>
    </order-header>
    <div class="wrapper">
      <div class="container">
        <div class="order-box">
          <loading v-if="loading"></loading>
          <div class="order" v-for="(item,index) in list" :key="index">
            <div class="order-title">
              <div class="item-info fl">
                {{item.createTime}}
                <span>|</span>
                {{item.receiverName}}
                <span>|</span>
                订单号：{{item.orderNo}}
                <span>|</span>
                {{item.paymentTypeDesc}}
              </div>
              <div class="item-money fr">
                <span>应付金额：</span>
                <span class="money">{{item.payment}}</span>
                <span>元</span>
              </div>
            </div>
            <div class="order-content clearfix">
              <div class="good-box fl" v-for="(s,index) in item.orderItemVoList" :key="index">
                <div class="good-list">
                  <div class="good-img">
                    <img v-lazy="s.productImage" alt />
                  </div>
                  <div class="good-name">
                    <div class="p-name">{{s.productName}}</div>
                    <div class="p-money">{{s.currentUnitPrice}} X {{s.quantity}}元</div>
                  </div>
                </div>
              </div>
              <div class="good-state fr" v-if="item.status == 10">
                <a href="javascript:;" @click="goPay(item.orderNo)">{{item.statusDesc}}</a>
              </div>
              <div class="good-state fr" v-else>
                <a href="javascript:;">{{item.statusDesc}}</a>
              </div>
            </div>
          </div>
          <!-- 分页器 -->
          <el-pagination
          class="pagination"
          background
          layout="total,prev, pager, next,jumper"
          :pageSize="pageSize"
          :total="total"
          @current-change = "handleChange"
          >
        </el-pagination>
        <!-- 按钮加载 -->
        <!-- <div class="load-more" v-if="showNextpage">
          <el-button type="primary" :loading="buttonloading" @click="loadmore">加载更多</el-button>
        </div> -->
        <!-- 下拉自动加载 -->
        <!-- <div class="scroll-more" v-infinite-scroll="scrollMore" infinite-scroll-disabled="busy" infinite-scroll-distance="410" v-show="buttonloading">
          <img src="/imgs/loading-svg/loading-spinning-bubbles.svg" alt="">
        </div> -->
        <no-data v-if="!loading&&list.length == 0"></no-data>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import OrderHeader from "../components/OrderHeader";
import Loading from "../components/Loading";
import NoData from "../components/NoData";
import { Pagination,Button } from "element-ui";
import infiniteScroll from 'vue-infinite-scroll';
export default {
  name: "order-list",
  components: {
    OrderHeader,
    Loading,
    NoData,
    [Pagination.name]:Pagination,
    [Button.name]:Button
  },
  directives:{infiniteScroll},
  data() {
    return {
      list: [],
      loading: true,
      pageSize:2,
      pageNum:1,
      total:0,
      buttonloading:false, 
      busy: false,//滚动加载是否触发
      showNextpage:true//控制加载更多按钮是否显示
    };
  },
  mounted() {
    this.getOrderList();
  },
  methods: {
    getOrderList() {
      //this.buttonloading = true;
      //this.busy = true;
      this.axios
        .get("/orders",{
          params:{
            pageSize:2,
            pageNum:this.pageNum
          }
        })
        .then(res => {
          //this.showNextpage = res.hasNextPage;
         //this.buttonloading = false;
         // this.busy = false;
          this.loading = false;
          this.list = res.list //分页器加载数据
          //this.list = this.list.concat(res.list);
          this.total = res.total;
        })
        .catch(() => {
          this.loading = false;
        });
    },
    goPay(orderNo) {
      //this.$router.push('/order/pay')
      // this.$router.push({
      //     path:'order-pay',
      //     query:{
      //         orderNo
      //     }
      // })
      this.$router.push({
        path: "/order/pay",
        query: {
          orderNo
        }
      });
    },
    //第一种方法：分页器
    handleChange(pageNum){
      this.pageNum = pageNum;
      this.getOrderList()
    },
    //第二种方法：加载更多按钮
    loadmore(){
      this.pageNum++;
      this.getOrderList()
    },
    //第三种方法，滚动加载通过npm插件实现
    scrollMore(){
      this.busy = true;
      setTimeout(()=>{
        this.pageNum++;
        this.getList();
      },500)
    },
    getList() {
      this.buttonloading = true;
      this.axios
        .get("/orders",{
          params:{
            pageSize:2,
            pageNum:this.pageNum
          }
        })
        .then(res => {
          this.buttonloading = false;
          this.list = this.list.concat(res.list);
          if(res.hasNextPage){
            this.busy=false
          }else{
            this.busy=true
          }
        })
    },
  }
};
</script>
<style lang="scss">
@import "./../assets/scss/config.scss";
@import "./../assets/scss/mixin.scss";
.order-list {
  .wrapper {
    background-color: $colorJ;
    padding-top: 33px;
    padding-bottom: 110px;
    .order-box {
      .order {
        @include border();
        background-color: $colorG;
        margin-bottom: 31px;
        &:last-child {
          margin-bottom: 0;
        }
        .order-title {
          height: 74px;
          line-height: 74px;
          background-color: $colorK;
          padding: 0 43px;
          font-size: 16px;
          color: $colorC;
          .item-info {
            span {
              margin: 0 9px;
            }
          }
          .money {
            font-size: 26px;
            color: $colorB;
          }
        }
        .order-content {
          padding: 0 43px;
          .good-box {
            width: 88%;
            .good-list {
              display: flex;
              align-items: center;
              height: 145px;
              .good-img {
                width: 112px;
                img {
                  width: 100%;
                }
              }
              .good-name {
                font-size: 20px;
                color: $colorB;
              }
            }
          }
          .good-state {
            height: 145px;
            line-height: 145px;
            font-size: 20px;
            color: $colorA;
            a {
              color: $colorA;
            }
          }
        }
      }
      .pagination {
        text-align: center;
      }
      .el-pagination.is-background .el-pager li:not(.disabled).active {
        background-color: #ff6600;
      }
      .el-button--primary {
        background-color: #ff6600;
        border-color: #ff6600;
      }
      .load-more,
      .scroll-more {
        text-align: center;
      }
    }
  }
}
</style>
