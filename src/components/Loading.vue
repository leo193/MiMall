<template>
    <div class="loading">
        <img src="/imgs/loading-svg/loading-bars.svg" alt="">
    </div>
</template>
<script>
export default {
    name:'loading'
}
</script>
<style lang="scss">
.loading{
    margin:40px 0 ;
    height: 80px;
    line-height: 80px;
    text-align: center;
    img{
        height: 100%;
    }
}
</style>