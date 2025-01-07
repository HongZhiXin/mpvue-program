<template>
  <div>
    <header>
      <picker @change="pickChange" :value="type" :range="rangesOptions">
        <view class="picker">
          {{type ? '销售' : '全部' }}<img src="../../../../assets/image/down.svg" />
        </view>
      </picker>
    </header>
    <content>
      <scroll-view :scroll-y="true" class="main-content" 	refresher-enabled>
        <div class="detail-card">
          <div>
            <div>
              <label>商品名：</label><span>康师傅茉莉蜜茶500ML</span>
            </div>
          </div>
          <div>
            <div>
              <label>变动前库存：</label><span>20</span>
            </div>
            <div>
              <label>变动库存：</label><span :class="'all'">-1</span>
            </div>
          </div>
          <div>
            <div>
              <label>变动方式：</label><span>20</span>
            </div>
            <div>
              <label>变动金额：</label><span :class="'all'">-8.000</span>
            </div>
          </div>
          <div>
            <div>
              <label>变动吧台：</label><span>吧台</span>
            </div>
          </div>
          <div>
            <div>
              <label>变动时间：</label><span>2024-12-11 14:15:28</span>
            </div>
          </div>
        </div>
      </scroll-view>
    </content>
  </div>
</template>
<script>
  export default {
    name: 'GoodStorageDetail',
    data(){
      return {
        type: ""
      }
    },
    computed: {
      rangesOptions(){
        return ['全部', '销售']
      }
    },
    methods: {
      pickChange(e) {
        const index = e.target.value
        if(index > 0) {
          this.type = 1
        } else {
          this.type = ""
        }
      }
    }
  }
</script>
<style scoped lang="scss">
  header {
    background-color: #F4F4F4;
    padding: 20rpx;
    border-bottom: 1rpx solid #bbbbbb;
    .picker {
      color: #7c7c7c;
      display: flex;
      align-items: center;
      justify-content: center;

    }
    img {
      width: 30rpx;
      height: 30rpx;
      margin-left: 9rpx;
      position: relative;
      top: 2px;
    }
  }
  .main-content {
    height: calc(100vh - 90px);
    .detail-card {
      padding: 14rpx 36rpx;
      background-color: #FFFFFF;
      margin-top: 16rpx;
      > div {
        line-height: 46rpx;
        font-size: 24rpx;
        > div {
          flex-basis: 50%;
        }
        span {
          color: #9B9B9B;
          &.all {
            color: red !important;
          }
        }
        display: flex;
      }
    }
  }
</style>
