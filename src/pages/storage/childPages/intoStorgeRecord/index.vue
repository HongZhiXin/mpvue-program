<template>
  <div class="intoStorgeRecordContainer">
    <header>
      <div>商品类型</div>
      <div>
        <picker mode="date" fields="month" :start="startDate" :end="endDate" :value="date" @change="datePickChange">
          <div> {{ date ? date : '时间选择' }}</div>
        </picker>
      </div>
      <div @click="showAddPanels('add')">添加</div>
    </header>
    <main>
      <actionCellRow v-for="(item, index) in list" :actions="item.action" :sign="index" :key="index" :data="item"
                     temp="2">
      </actionCellRow>
    </main>
  </div>
</template>
<script>
import ActionCellRow from "@/components/action-cell-row";
import dayjs from "dayjs";

export default {
  name: "IntoStorgeRecord",
  components: {ActionCellRow},
  data() {
    return {
      list: [],
      date: ""
    }
  },
  computed: {
    startDate() {
      return dayjs().subtract(3, 'year').format("YYYY-MM")
    },
    endDate() {
      return dayjs().subtract(-6, 'month').format("YYYY-MM")
    }
  },
  methods: {
    datePickChange(e) {
      console.log(e)
      this.date = e.target.value
    },
    showAddPanels(type = 'add') {
      if (type === 'copy') {
        wx.navigateTo({
          url: "/pages/storage/childPages/goodIntoStorageForm/main?formType=" + type
        })
        return
      }
      wx.showActionSheet({
        itemList: ['入库商品', '从采购订单导入'],
        success: result => {
          if (result.tapIndex === 0) {
            wx.navigateTo({
              url: "/pages/storage/childPages/goodIntoStorageForm/main?formType=" + type
            })
          }
        }
      })
    },

  },
  mounted() {
    this.date = dayjs().format("YYYY-MM")
    this.list = Array(12).fill(0).map(i => ({
      action: [{btnName: '删除', type: 'warning'},
        {btnName: '新增', type: 'primary'},
        {
          btnName: '复制', type: 'text', click: () => {
            this.showAddPanels('copy')
          }
        },]
    }))
  }
}
</script>
<style lang="scss">
.intoStorgeRecordContainer {
  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    height: 50px;
    background-color: #f7f7f7;
    border-bottom: 1rpx solid #bbbbbb;
    position: fixed;
    top: 0;
    width: 100vw;
    z-index: 99;

    > div {
      font-size: 27rpx;
      color: #2C2D30;

      &:nth-child(1) {
        margin-left: 12px;
      }

      &:nth-child(3) {
        margin-right: 12px;
      }
    }
  }

  main {
    height: calc(100vh - 50px);
    overflow: hidden auto;
    margin-top: 50px;
    padding-bottom: 10px;
  }

  .record-item {
    background-color: #FFFFFF;
    margin-top: 24rpx;
    padding: 10rpx 22rpx;

    > div {
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-size: 26rpx;
      color: #9B9B9B;
      line-height: 60rpx;

      span {
        color: #2C2D30;
      }

      &:nth-child(1) {
        border-bottom: 1rpx solid #bbbbbb;

        > div:first-child > span:first-child {
          border: 1px solid #9B9B9B;
          padding: 2px 4px;
          margin-right: 6px;
        }
      }
    }
  }
}
</style>
