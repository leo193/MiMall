<template>
  <div class="footer">
    <div class="footer-logo">
      <img src="/imgs/logo-footer.png" alt />
      <p>小米商城</p>
    </div>
    <div class="footer-link">
      <a href="http://www.unicornfordesign.com" target="_blank">孤角兽</a>
      <span>|</span>
      <a href="http://www.yuefenqu.com" target="_blank">悦分趣</a>
      <span>|</span>
      <a href="http://www.ec-h.com.cn" target="_blank">欧洲艺术交流中心</a>
    </div>
    <div class="copyright">Copyright ©2019 <span>mi.com</span> 京ICP证110507号</div>
  </div>
</template>
<script>
export default {
  name: "nav-footer"
};
</script>
<style lang="scss">
@import "../assets/scss/base.scss";
@import "../assets/scss/mixin.scss";
@import "../assets/scss/config.scss";
.footer {
  height: 234px;
  border-top: 4px solid $colorA;
  background: $colorB;
  color: $colorD;
  font-size: $fontI;
  text-align: center;
  .footer-logo{
      margin-top:46px;
      margin-bottom: 31px;
      img{
          width:53px;
          height: 36px;
          margin-bottom: 13px;
      }
  }
  .footer-link{
      a{
          color:$colorD;
          display:inline-block;
      }
      span{
          margin:0 10px;
      }
      margin-bottom: 13px;
  }
  .copyright{
      span{
          color:$colorA;
      }
  } 
}
</style>