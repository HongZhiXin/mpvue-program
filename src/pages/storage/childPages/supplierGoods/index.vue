<template>
  <scroll-view class="main-container" :scroll-y="true">
    <div class="good-item-detail" v-for="good in list">
      <img src="http://assets.topfreeweb.net/shop/templates/1287370599462.jpg"/>
      <div>
        <div>{{ good.name }}</div>
        <div>进货均价：<span>{{ good.price1 }}</span>&nbsp;&nbsp;市场均价：<span>{{ good.price2 }}</span></div>
      </div>
    </div>
  </scroll-view>
</template>
<script>
export default {
  name: "SupplierGoods",
  data() {
    return {
      list: []
    }
  },
  mounted() {
    this.list = Array(12).fill(1).map(i => ({
      name: '红牛',
      price1: '3.000',
      price2: '6'
    }))
  }
}
</script>
<style lang="scss" scoped>
.main-container {
  height: calc(100vh - 40rpx);
  padding: 20rpx 0;
  border-top: 1rpx solid #bbbbbb;

  .good-item-detail {
    display: flex;
    align-items: center;
    padding: 10rpx 18rpx;
    border-bottom: 1rpx solid #bbbbbb;
    background-color: #FFFFFF;

    img {
      width: 120rpx;
      height: 120rpx;
    }

    div {
      font-size: 26rpx;
      color: #9B9B9B;

      > div {
        &:first-child {
          font-size: 29rpx;
          color: #2C2D30;
          margin-bottom: 14rpx;
        }

        span {
          color: #2C2D30;
        }
      }
    }
  }
}
</style>
