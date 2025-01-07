<template>
  <div class="form-container">
    <form>
      <div style="margin: 10px 0" class="sub-div">
        <div class="form-cell">
          <span>启用库存管理</span>
          <switch v-model.lazy="source.filed1"/>
        </div>
        <div class="form-cell">
          <span>启用负库存</span>
          <switch v-model.lazy="source.filed2"/>
        </div>
        <div class="form-cell">
          <span>商品区分货架库存</span>
          <switch v-model.lazy="source.filed3"/>
        </div>
      </div>
      <div style="margin: 10px 0" class="sub-div">
        <div class="form-cell">
          <span>启用原料库管理</span>
          <switch v-model.lazy="source.filed4"/>
        </div>
        <div class="form-cell">
          <span>启用原料库负库存</span>
          <switch v-model.lazy="source.filed5"/>
        </div>
      </div>
      <div style="margin: 10px 0" class="sub-div">
        <div class="form-cell">
          <span>盘点时采用盲点模式</span>
          <switch v-model.lazy="source.filed1"/>
        </div>
        <div class="form-cell">
          <span>上/下架需收银员确认</span>
          <switch v-model.lazy="source.filed2"/>
        </div>
      </div>
      <div style="margin: 10px 0" class="sub-div">
        <div class="form-cell">
          <span>采购计划审批人</span>

          <picker :value="rangeIndex1" :range="rangesOptions" @change="pickChange">
            <view class="picker">
             {{rangeIndex1 ? rangesOptions[rangeIndex1] : '请选择' }} >
            </view>
          </picker>
        </div>
        <div class="form-cell">
          <span>是否为连锁审批模式</span>
          <switch v-model.lazy="source.filed2"/>
        </div>
        <div class="form-cell">
          <span>总部采购计划审批人</span>
          <switch v-model.lazy="source.filed1"/>
        </div>
      </div>
      <div class="sub-div">
        <div class="form-cell">
          <span>售罄不显示</span>
          <switch v-model.lazy="source.filed7"/>
        </div>
        <div class="tip">
          小提示
          <div>启用货架库存后，货架上库存需通过“商品/原料上下架”功能进行增加或减少。</div>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: 'StorageBasic',
  data() {
    return {
      source: {
        filed1: false,
        filed2: false,
        filed3: false,
        filed4: false,
        filed5: false,
        filed6: false,
        filed7: false,
      },
      rangeIndex1: undefined,
      ranges: [
        {label: '方兵', value: '1'},
        {label: '陈自海', value: '2'},
        {label: '武穹', value: '3'}
      ]
    }
  },
  computed: {
    rangesOptions(){
      return this.ranges.map(r => r.label)
    }
  },
  methods: {
    pickChange(e){
      const index = e.target.value
      this.source.filed6 = this.ranges[index].value
      this.rangeIndex1 = index
    }
  }
}
</script>

<style lang="scss" scoped>
.form-container {
  .sub-div {
    background-color: #FFFFFF;
    &:last-child {
      margin-top: 10px;
    }
    .tip {
      padding: 0 24rpx;
      font-size: 26rpx;
      color: #999999;
    }
  }
}
</style>
