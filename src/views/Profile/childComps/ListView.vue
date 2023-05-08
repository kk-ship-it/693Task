<template>
    <div class="list">
        <div class="user-own">
            <div class="money">
                <div><span>0</span>个</div>
                <div class="text">我的收藏</div>
            </div>
            <div class="discount">
                <div><span>0</span>个</div>
                <div class="text">我的关注店铺</div>
            </div>
            <div class="point">
                <div><span>0</span>分</div>
                <div class="text">我的积分</div>
            </div>
        </div>
        <div class="list-view">
            <div class="mes">
                <img src="~assets/img/profile/message.svg" alt="">
                <span>我的消息</span>
            </div>
      
            <div class="vip">
                <img src="~assets/img/profile/vip.svg" alt="">
                <span>代发货</span>
            </div>
            <div class="vip">
                <img src="~assets/img/profile/cart.svg" alt="">
                <span>待收货</span>
            </div>
            <div class="shop">
                <img src="~assets/img/profile/shopping.svg" alt="">
                <span>待评价</span>
            </div>
            <div class="pointer">
                <img src="~assets/img/profile/pointer.svg" alt="">
            <span>退款/售后</span>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'ListView'
}
</script>

<style>
.user-own {
    height: 83px;
    display: flex;
    text-align: center;
    padding: 20px 0;
}
.money, .discount, .point {
    flex: 1;
    line-height: 26px;
}
.user-own span {
    color: #ff5f3e;
    font-size: 24px;
    font-weight: bolder;
}
.user-own .text {
    font-size: 12px;
}
.list-view {
    margin: 30px 15px 0;
}
.list-view div {
    border-bottom: 1px solid #e7e7e7;
}
.list-view span {
    display: inline-block;
    height: 44px;
    line-height: 44px;
}
.list-view img {
    width: 18px;
    margin-right: 10px;
    margin-top: 10px;
}
</style>
