<template>
  <div class="inventoryContainer">
    <main>
      <div class="item">
        <div>
          <span>吧台</span>
          <img src="../../../../assets/image/edit.svg" @click="openPageContainer('edit')"/>
        </div>
        <div>
          <p>
            <div>吧台IP：</div>
            <span>192.168.18.223</span>
          </p>
          <p>
            <div>管辖机号：</div>
            <span></span>
          </p>
        </div>
      </div>
    </main>
    <footer>
      <button @click="openPageContainer()" type="primary">添加</button>
    </footer>
    <page-container :show="showPageContainer" position="right" @leave="onAfterLeave">
      <div class="inventory-form">
        <div class="form-cell">
          <span>货架名称</span>
          <input placeholder="请输入货架名称"/>
        </div>
        <div class="form-cell">
          <span>关联吧台</span>
          <input placeholder="请输入订单处理吧台IP"/>
        </div>
        <div class="form-cell">
          <span>货架类型</span>
          <input/>
        </div>
        <div class="form-cell">
          <span>货架名称</span>
          <input/>
        </div>
        <div class="p">
          <div>管辖机号</div>
          <textarea placeholder="例如: 1-5,6,8,9-10"/>
        </div>
        <button type="primary">
          保存
        </button>
      </div>
    </page-container>
  </div>
</template>

<script>
export default {
  name: "",
  data() {
    return {
      showPageContainer: false,
      formType: 'add'
    }
  },
  methods: {
    onAfterLeave() {
      this.showPageContainer = false
      wx.setNavigationBarTitle({title: '货架管理'})
    },
    openPageContainer(type = 'add') {
      this.showPageContainer = true
      this.formType = type
      wx.setNavigationBarTitle({
        title: type === 'add' ? '添加货架' : '修改货架'
      })
    }
  }
}
</script>
<style lang="scss">
.inventoryContainer {
  padding-top: 10px;

  footer {
    position: fixed;
    bottom: 0;
    width: 100%;
    background-color: #FFFFFF;
    height: 56px;
    line-height: 56px;
    text-align: center;
    padding-top: 16px;
    button {
      width: 88%;
    }
  }

  .item {
    background-color: #FFFFFF;
    padding: 10px 14px;

    > div {
      &:first-child {
        display: flex;
        justify-content: space-between;
        align-items: center;
        font-size: 32rpx;
        margin-bottom: 10px;
      }

      &:nth-child(2) {
        font-size: 26rpx;
        color: #9B9B9B;

        div {
          line-height: 20px;
        }
      }
    }

    img {
      width: 20px;
      height: 20px;
    }
  }
}

.inventory-form {
  border-top: 1rpx solid #bbbbbb;
  height: 100vh;
  > .p {
    padding: 0 24rpx;
    color: #9B9B9B;

    div {
      margin: 10px 0;
      font-size: 22rpx;
    }
    textarea {
      border-radius: 8px;
      background-color: #FFFFFF;
      width: calc(100% - 22px);
      border: 1rpx solid #bbbbbb;
      padding: 10px;
    }
  }
  button {
    width: 86%;
    margin-top: 20px;
  }
}
</style>
