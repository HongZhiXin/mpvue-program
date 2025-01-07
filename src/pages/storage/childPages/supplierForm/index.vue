<template>
    <div class="form-container">
      <div>
        <div class="form-cell">
          <span>供应商名称</span>
          <input placeholder="请输入"/>
        </div>
        <div class="form-cell">
          <span>供货周期</span>
          <div class="right-control-div">
            <input placeholder="请输入" v-model.lazy="form.days" />
            <span>天</span>
          </div>
        </div>
        <div class="form-cell">
          <span>结款周期</span>
          <picker :range="ranges" :value="form.type" @change="pickChange">
            <view class="picker">
              {{ supplierType ? supplierType : '请选择'}}
            </view>
          </picker>
        </div>
        <div class="form-cell">
          <span>供应商电话</span>
          <input placeholder="请输入" />
        </div>
        <div class="form-cell">
          <span>供应商地址</span>
          <input placeholder="请输入" />
        </div>
      </div>

      <div>
        <span>备注</span>
        <div>
          <textarea :auto-height="true" placeholder="请输入备注" />
        </div>
      </div>

      <button block type="primary">保存</button>
    </div>
</template>
<script>
export default {
  name: '',
  data() {
    return {
      isEdit: false,
      form: {
        name: '',
        days: '0',
        phone: '',
        address: '',
        remark: '',
        type: ''
      },
      ranges: ['现结', '挂账', '上打下', '月结', '季节']
    }
  },
  methods: {
    pickChange(e) {
      this.form.type = e.target.value
    }
  },
  computed: {
    supplierType() {
      return  this.form.type+'' ? {
        0: '现结', 1: '挂账', 2: '上打下', 3: '月结', 4: '季节'
      }[this.form.type] : ''
    },
  },
  onLoad(options) {
    this.isEdit = !!options.id
    wx.setNavigationBarTitle({title: this.isEdit ? '修改供应商' : '新增供应商'})
  }
}
</script>
<style lang="scss" scoped>
.form-container {
  margin-top: 2rpx;
  > div {
    &:nth-child(1) {
      background-color: #FFFFFF;
    }
    &:nth-child(2) {
      margin-top: 20rpx;
      span {
        padding-left: 20rpx;
        font-size: 26rpx;
        color: #9B9B9B;
        & + div {
          background-color: #FFFFFF;
          min-height: 180rpx;
          textarea {
            width: 100%;
            padding: 20rpx;
            color: #656565;
            margin-top: 20rpx;
          }
        }
      }
    }
  }
  button {
    width: 80%;
    margin-top: 30rpx;
  }
}
</style>
