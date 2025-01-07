<template>
  <div>
    <div class="add-form-container">
      <div class="form-div">
        <div class="form-cell">
          <span>供应商</span>
          <input/>
        </div>
        <div class="form-cell">
          <span>自动上架到</span>
          <input/>
        </div>
      </div>
      <div>
        <span>商品信息</span>
        <div class="goods">
          <active-cell-row  v-for="(good, i) in goodsList" :sign="i"
                            :key="i" :actions="actions" :data="good" temp="1">

          </active-cell-row>
        </div>
        <div>
          <span @click="onChooseScanCode">扫码添加商品</span>
          <span @click="onHandSelect">手动添加商品</span>
        </div>
      </div>
      <div class="form-div">
        <div class="form-cell">
          <span>支付方式</span>
          <input/>
        </div>
        <div class="form-cell">
          <span>应付金额</span>
          <input/>
        </div>
        <div class="form-cell">
          <span>实付金额</span>
          <input/>
        </div>
      </div>
      <div>
        <span>备注</span>
        <textarea placeholder="请输入备注信息" />
      </div>
      <button type='primary'>确定</button>
    </div>
    <page-container :show="showPageContainer" position="right" @leave="onAfterLeave">
      <div class="handSelectPage">
        <header>
          <picker>
            <div class="picker">
              <span>全部商品</span><img src="../../../../assets/image/down.svg" />
            </div>
          </picker>
          <div>
            <img src="../../../../assets/image/search.svg" />
            <input placeholder="简拼/编号/商品名" />
          </div>
        </header>
        <main>
          <div class="good-item">
            <img />
            <div>
              <div>烤肠</div>
              <div>
                <span>库存：336个</span>
                <span>单价：2.00</span>
                <span>保质期：0天</span>
              </div>
            </div>
            <span @click="onClickGoodRow">
               <img src="../../../../assets/image/plus.svg" />
            </span>
          </div>
          <div class="good-item">
            <img />
            <div>
              <div>烤肠</div>
              <div>
                <span>库存：336个</span>
                <span>单价：2.00</span>
                <span>保质期：0天</span>
              </div>
            </div>
          </div>
        </main>
        <footer>
          <span class="empty">列表是空的</span>
          <span>选好了</span>
          <img src="../../../../assets/image/checklist.svg">
        </footer>

        <div v-if="showPageModal" class="modal-mask">
          <div>
            <p>烤肠</p>
            <div class="form-cell">
              <span>库存数量</span>
              <input />
            </div>
            <div class="form-cell">
              <span>发生数量</span>
              <input />
            </div>
            <div class="form-cell">
              <span>发生单价</span>
              <input />
            </div>
            <div class="form-cell">
              <span>发生金额</span>
              <input />
            </div>
            <div class="form-cell">
              <span>生产日期</span>
              <input />
            </div>
            <div>
              <span @click="onCloseModal">取消</span>
              <span>确定</span>
            </div>
          </div>
        </div>
      </div>
    </page-container>
  </div>
</template>

<script>

import ActiveCellRow from "../../../../components/action-cell-row.vue";

export default {
  name: "goodIntoStorageForm",
  components: {ActiveCellRow},
  data() {
    return {
      formType: '',
      addForm: {},
      showPageContainer: false,
      showPageModal: false,
      goodsList: [],
    }
  },
  methods: {
    onChooseScanCode(){
      wx.scanCode({
        success: result => {

        }
      })
    },
    onHandSelect(){
      this.showPageContainer = true
      wx.setNavigationBarTitle({
        title: '添加商品'
      })
    },
    onAfterLeave(){
      this.showPageContainer = false
      wx.setNavigationBarTitle({
        title: '商品入库'
      })
    },
    onClickGoodRow(item){
      this.showPageModal = true
    },
    onCloseModal(){
      this.showPageModal = false
    },
  },
  computed: {
    actions() {
      return [{btnName: '删除', type: 'warning', click: (v) => {
          console.log(v)
        }}]
    },
  },
  mounted() {
    const query = this.$root.$mp.query
    const {formType} = query
    this.formType = formType
    wx.setNavigationBarTitle({
      title: '商品入库'
    })
    if(this.formType === 'copy') {
      this.goodsList = [
        {goodName: "矿泉水"},
        {goodName: "东鹏特饮能量型饮料500ML"},
        {goodName: "战马"},
        {goodName: "红牛"},
      ]
    } else {
      this.goodsList = []
    }
  }
}
</script>

<style lang="scss">
.add-form-container {
  padding-bottom: 10px;
  > div{
    &.form-div {
      background-color: #FFFFFF;
    }
    &:not(.form-div) {
      margin-bottom: 20px;
      > span {
        padding: 0 24rpx;
        color: #9B9B9B;
        font-size: 24rpx;
        margin: 10px 0;
        display: block;
      }
      > div:not(.goods) {
        background-color: #FFFFFF;
        padding: 20rpx 34rpx;
        display: flex;
        align-items: center;
        justify-content: center;
        color: #4EAA31;
        > span {
          display: block;
          flex: 1;
          text-align: center;
          &:nth-child(1) {
            border-right: 1rpx solid #bbbbbb;
          }
        }
      }
    }
    textarea {
      background-color: #FFFFFF;
      width: 100%;
      padding: 18rpx 24rpx;
    }
  }

  button {
    width: 80%;
  }

  .goods {
     div.good-card {
      display: flex;
      align-items: center;
      background-color: #FFFFFF;
      border-bottom: 1rpx solid #bbbbbb;
       &:active {
         background-color: rgba(178, 178, 178, 0.1);
       }
      > img {
        width: 50px;
        height: 50px;
      }
      > div > div {
        margin-bottom: 4px;
      }
      span {
        color: #9B9B9B;
        font-size: 26rpx;
        &:nth-child(3) {
          margin: 0 14px;
        }
      }
    }
  }
}

.handSelectPage {
  height: 100vh;
  width: 100vw;
  background-color: #f7f7f7;
  header {
    padding: 14rpx 24rpx;
    font-size: 26rpx;
    display: flex;
    align-items: center;
    border-bottom: 1rpx solid #bbbbbb;
    img {
      width: 32rpx;
      height: 32rpx;
    }
    .picker {
      display: flex;
      align-items: center;
    }
    > div {
      flex: 1;
      background-color: #FFFFFF;
      border-radius: 8px;
      padding: 10rpx;
      display: flex;
      align-items: center;
      margin-left: 10px;
      img {
        margin-right: 6px;
      }
      input {
        width: 100%;
      }
    }
  }
  main {
    padding-top: 6rpx;
    .good-item {
      display: flex;
      align-items: center;
      background-color: #FFFFFF;
      padding: 8rpx 18rpx;
      &:not(:last-child) {
        border-bottom: 1rpx solid #bbbbbb;
      }
      > img {
        width: 54rpx;
        height: 54rpx;
        margin-right: 20rpx;
      }
      > div {
        font-size: 25rpx;
        color: #9B9B9B;
        > div {
          &:first-child {
            font-size: 30rpx;
            color: #2C2D30;
            margin-bottom: 10rpx;
          }
        }
        span {
          &:nth-child(2) {
            margin: 0 14rpx;
          }
        }
        flex: 1;
      }
      > span {
        display: block;
        height: 100%;
        padding: 0 20rpx;
        img {
          width: 50rpx;
          height: 50rpx;
        }
      }
    }
  }
  footer {
    position: fixed;
    width: 100%;
    bottom: 0;
    display: flex;
    align-items: center;
    justify-content: space-between;
    height: 60px;
    box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.3);
    > span {
      display: block;
      &:nth-child(1) {
        margin-left: 60px;
        &.empty {
          color: #9B9B9B;
          font-size: 26rpx;
        }
      }
      &:nth-child(2) {
        padding:0  20px;
        background-color: #4EAA31;
        color: #FFFFFF;
        opacity: .8;
        height: 100%;
        line-height: 60px;
      }
    }
    img {
      width: 60px;
      height: 60px;
      position: absolute;
      top: -5px;
    }
  }
  .modal-mask {;
    background-color: rgba(0,0,0, 0.4);
    width: 100vw;
    height: 100vh;
    position: absolute;
    top: 0;
    left: 0;
    > div {
      position: absolute;
      top: 50%;
      left: 50%;
      width: 78%;
      transform: translate(-50%, -50%);
      background-color: #FFFFFF;
      border-radius: 6px;
      padding: 20px 10px 0;
      z-index: 999;
      > div {
        &:last-child {
          display: flex;
          align-items: center;
          span {
            display: flex;
            flex: 1;
            justify-content: center;
            align-items: center;
            padding: 10px;
            &:last-child {
              border-left: 1rpx solid #bbbbbb;
              color: #4EAA31;
            }
          }
        }
      }
    }
    .form-cell {
      width: calc(100% - 48rpx);
    }
    p {
      margin: 4px 0;
      text-align: center;
    }
  }
}
</style>
