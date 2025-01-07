<template>
  <div class="container">
    <div class="fixed-header">
      <div>
        <div class="input-div">
          <img src="../../../../assets/image/search.svg"  />
          <input placeholder="简拼/编号/商品名" v-model.lazy="keyword" confirm-type="search" />
        </div>
        <img src="../../../../assets/image/scan.svg" @click="openScanAction" />
        <img src="../../../../assets/image/shaixuan.svg" @click="openScanAction" />
      </div>
      <div>
        <div>
          <span>库存商品数</span>
          <span>8210</span>
        </div>
        <div>
          <span>库存成本总计</span>
          <span>20654.1235</span>
        </div>
        <div>
          <span>库存销售毛利</span>
          <span>6908.11</span>
        </div>
        <div>
          <span>预警商品数</span>
          <span>210</span>
        </div>
      </div>
    </div>
    <scroll-view class="goods-container" >
      <div class="good-item" v-for="(good, index) in goodList" :key="index" @click="navToDetail">
        <div>
          <img src="http://assets.topfreeweb.net/shop/templates/1287370599462.jpg" />
          <div>
            <div>{{ good.goodName }}</div>
            <div>进货价：<span>4.000</span>&nbsp;&nbsp;零售价：<span>3.00</span>&nbsp;&nbsp;毛利：<span>1.00</span></div>
            <div>库存额：<span>0.00</span>&nbsp;&nbsp;库存毛利：<span>0.00</span></div>
            <div>近10天日均销售数：<span>65</span></div>
            <div>库存可销售天数：<span>1</span>天</div>
          </div>
        </div>
        <div>
          <div>
            <span>库存合计：</span>
            <span>{{good.storage1}}瓶</span>
          </div>
          <div>
            <span>主仓库：</span>
            <span>{{good.storage2}}瓶</span>
          </div>
          <div>
            <span>吧台：</span>
            <span>{{good.storage3}}瓶</span>
          </div>
        </div>
      </div>
    </scroll-view>
  </div>
</template>

<script>
export default {
  name: "GoodsListStorage",
  data() {
    return {
      keyword: "",
      goodList: [],
    }
  },
  methods: {
    openScanAction() {
      wx.scanCode({
        scanType: ['barCode'],
        success: result => {
          if(result.result) {
            this.keyword = result.result
          }
        },
        fail: err => {
          console.log(err)
        }
      })
    },
    navToDetail(){
      wx.navigateTo({
        url: '/pages/storage/childPages/goodDetail/main'
      })
    },
  },
  onReachBottom() {
    console.log('监听用户上拉加载')
    if(this.goodList.length >= 30) {
      return
    }
    wx.showLoading({
      title: '数据加载中'
    })
    const mock = Array(10).fill(0).map(i => ({
      goodName: '康师傅茉莉蜜茶500ML',
      storage1: (Math.random() * 10).toFixed(0),
      storage2: (Math.random() * 10).toFixed(0),
      storage3: (Math.random() * 10).toFixed(0),
    }))
    this.goodList.push(...mock)
    setTimeout(() => {
      wx.hideLoading()
    }, 1000)
  },
  created(){
    const mock = Array(10).fill(0).map(i => ({
      goodName: '康师傅茉莉蜜茶500ML',
      storage1: (Math.random() * 10).toFixed(0),
      storage2: (Math.random() * 10).toFixed(0),
      storage3: (Math.random() * 10).toFixed(0),
    }))
    this.goodList.push(...mock)
  }
}
</script>
<style lang="scss" scoped>
.container {
  height: 1000px;

  .fixed-header {
    position: fixed;
    top: 0;
    z-index: 99;
    background-color: #F4F4F4;
    > div {
      &:first-child {
        padding: 10px 18px;
        display: flex;
        align-items: center;

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

        > img {
          width: 28px;
          height: 28px;
          margin-left: 5px;
        }
      }

      &:nth-child(2) {
        display: flex;
        background-color: #FFFFFF;
        border-top: 1rpx solid #bbbbbb;
        border-bottom: 1rpx solid #bbbbbb;
        font-size: 26rpx;

        > div {
          flex: 1;
          padding: 12rpx 10rpx;
          span {
            display: block;
            text-align: center;
            line-height: 20px;
          }
          &:not(:last-child){
            border-right: 1rpx solid #bbbbbb;
          }
        }
      }
    }
  }

  .goods-container {
    margin-top: 100px;
    padding-bottom: 10px;
    .good-item {
      background-color: #FFFFFF;
      margin-top: 10px;
      > div {
        &:first-child {
          display: flex;
          align-items: center;
          padding: 30rpx;
          border-bottom: 1rpx solid #e7e7e7;
          img {
            width: 160rpx;
            height: 160rpx;
          }
          font-size: 26rpx;
          color: #9B9B9B;
          > div > div {
            line-height: 40rpx;
            &:first-child {
              letter-spacing: 3rpx;
              color: #000000;
              font-size: 34rpx;
              margin-bottom: 16rpx;
            }
            &:last-child {
              border: 1px dashed #9B9B9B;
              display: inline-block;
              padding: 2rpx 8rpx;
            }
            span {
              color: #000000;
            }
          }
        }
        &:nth-child(2){
          font-size: 26rpx;
          > div {
            display: flex;
            justify-content: space-between;
            padding: 20rpx 30rpx;
            border-bottom: 1rpx solid #e7e7e7;
            span {
              &:nth-child(2){
                color: #9B9B9B;
              }
            }
          }
        }
      }
    }
  }
}
</style>
