<template>
  <div>
    <header>
      <div class="input-div">
        <img src="../../../../assets/image/search.svg"  />
        <input placeholder="供应商名称/备注/商品名称搜索" v-model.lazy="keyword" confirm-type="search" />
      </div>
      <span @click="navToFormPage()">添加</span>
    </header>
    <main>
      <div class="supplier-item">
        <div>
          <div>红牛厂家</div>
          <div>电话：<span>18999999919</span></div>
          <div>供货品类：<span>28</span> &nbsp;&nbsp;供货周期：<span>10</span>天&nbsp;&nbsp;现结</div>
        </div>
        <footer>
          <span @click="navToGoodsDetail">供应商品明细</span>
          <span @click="navToFormPage('3')">修改供应商信息</span>
        </footer>
      </div>
    </main>
  </div>
</template>
<script>
export default {
  name: '',
  data(){
    return {
      keyword: ""
    }
  },
  methods: {
    navToGoodsDetail(){
      wx.navigateTo({
        url: '/pages/storage/childPages/supplierGoods/main'
      })
    },
    navToFormPage(id = "") {
      wx.navigateTo({
        url: `/pages/storage/childPages/supplierForm/main${id ? '?id=' + id : ''}`
      })
    }
  }
}
</script>
<style scoped lang="scss">
  header {
    padding: 10px 18px;
    display: flex;
    align-items: center;
    border-bottom: 1rpx solid #bbbbbb;
    .input-div {
      width: calc(100vw - 90px);
      background-color: #FFFFFF;
      padding: 6rpx;
      border-radius: 6px;
      display: flex;
      align-items: center;
      font-size: 26rpx;
      img {
        width: 18px;
        height: 18px;
        margin-right: 8rpx;
      }
      input {
        width: 100%;
      }
    }
    > span {
      font-size: 26rpx;
      color: #5d5d5d;
      margin-left: 10px;
    }

  }
  main {
    margin-top: 10px;
    .supplier-item {
      background-color: #FFFFFF;
      > div {
        padding: 20rpx 0;
        &:first-child{
          padding-left: 130rpx;
          > div {
            font-size: 26rpx;
            color: #9B9B9B;
            line-height: 40rpx;
            &:nth-child(1) {
              font-size: 32rpx;
              color: #2C2D30;
              line-height: 50rpx;
            }
            span {
              color: #2C2D30;
            }
          }
        }
      }
      footer {
        display: flex;
        align-items: center;
        padding: 20rpx;
        border-top: 1rpx solid #bbbbbb;
        span {
          display: block;
          text-align: center;
          flex: 1;
          font-size: 26rpx;
          color: #00CB91;
          &:first-child {
            border-right: 1rpx solid #bbbbbb;
          }
        }
      }
    }
  }
</style>
