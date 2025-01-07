<template>
  <div class="container">
    <div class="row-menu-div">
      <p>基础配置</p>
      <div class="row-menu-container">
        <div class="row-menu" @click="customJump('basic')">
          <img src="../../assets/image/settings.svg" />
          <div>基础配置</div>
        </div>
        <div class="row-menu"  @click="customJump('supplier')">
          <img src="../../assets/image/settings.svg" />
          <div>供应商管理</div>
        </div>
      </div>
    </div>
    <div class="row-menu-div">
      <p>商品入库</p>
      <div class="row-menu-container">
        <div class="row-menu">
          <img src="../../assets/image/settings.svg" />
          <div>采购订单</div>
        </div>
        <div class="row-menu" @click="customJump('intoStorgeRecord')">
          <img src="../../assets/image/settings.svg" />
          <div>入库单</div>
        </div>
      </div>
    </div>
    <div class="row-menu-div">
      <p>库存管理</p>
      <div class="row-menu-container">
        <div class="row-menu" @click="customJump('inventory')">
          <img src="../../assets/image/settings.svg" />
          <div>货架管理</div>
        </div>
        <div class="row-menu">
          <img src="../../assets/image/settings.svg" />
          <div>上下架</div>
        </div>
        <div class="row-menu" @click="customJump('goods')">
          <img src="../../assets/image/settings.svg" />
          <div>商品库存</div>
        </div>
        <div class="row-menu">
          <img src="../../assets/image/settings.svg" />
          <div>吧台库存</div>
        </div>
      </div>
    </div>
    <div class="row-menu-div">
      <p>商品出库</p>
      <div class="row-menu-container">
        <div class="row-menu">
          <img src="../../assets/image/settings.svg" />
          <div>退货单</div>
        </div>
        <div class="row-menu">
          <img src="../../assets/image/settings.svg" />
          <div>报损单</div>
        </div>
        <div class="row-menu">
          <img src="../../assets/image/settings.svg" />
          <div>盘点商品</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Storage',
    data() {
      return {

      }
    },
    methods: {
      customJump(pageName) {
        wx.navigateTo({
          url: `/pages/storage/childPages/${pageName}/main`
        })
      }
    }
  }
</script>

<style lang="scss" scoped>
  .container {
    background-color: #FFFFFF;
    padding: 20px 0;
    .row-menu-div {
      p {
        color: #808080;
        font-size: 24rpx;
        display: flex;
        align-items: center;
        &::before {
          content: '';
          width: 4px;
          height: 12px;
          background-color: #54deee;
          display: block;
          margin-right: 12px;
        }
      }
    }

    .row-menu-container {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 10px 18px;
      margin: 14px 0;
      .row-menu {
        display: flex;
        flex-direction: column;
        justify-items: center;
        align-items: center;
        flex: 1;
        img {
          width: 64rpx;
          height: 64rpx;
        }
        div {
          margin-top: 10px;
          text-align: center;
          font-size: 28rpx;
          color: #010101;
        }
      }


    }
  }
</style>
