<template>
  <div :class="'has-action-row' + ' action' + sign" @touchstart="touchStart" @touchmove="touchMove"
       @touchend="touchEnd" v-bind:style="{transform: 'translateX('+ distance +'px)'}">
    <template v-if="temp === '1'">
      <div class="good-card">
        <img />
        <div>
          <div>{{ data.goodName }}</div>
          <span>发生数量: 264瓶</span>
          <span>发生单价: 2.00</span>
          <span>小计: 528.00</span>
        </div>
      </div>
    </template>
    <template v-else-if="temp === '2'">
      <div class="record-item" >
        <div>
          <div>
            <span>商品</span>
            <span>红牛厂家</span>
          </div>
          <div>
            2024-12-11 14:56
          </div>
        </div>
        <div>
          <div>
            <span>单号：</span>20241211145615208
          </div>
          <div>
            <span>支付方式：</span>现金
          </div>
        </div>
      </div>
    </template>
    <div class="active-panel"  v-bind:style="{width: initPanelMargin + 'px'}">
      <div v-for="(action, a) in actions" @click="action.click(sign)"
          :key="a" :class="{warning: action.type === 'warning' , primary: action.type === 'primary', text: action.type === 'text' }">
        {{ action.btnName }}
      </div>
    </div>
  </div>
</template>
<script>

import {transform} from "lodash/object";

export default {
  name: "active-cell-row",
  props: {
    actions: {
      default: () => [],
      type: Array,
    },
    sign: {
      default: "0",
      type: String,
    },
    data: {
      default: () => ({}),
      type: Object
    },
    temp: {
      default: "0",
      type: String,
    }
  },
  data() {
    return {
      x: 0,
      y: 0,
      distance: 0,
      isMoved: false,
      showBtnList: false
    }
  },
  computed: {
    initPanelMargin() {
      return this.actions.length * 60
    }
  },
  methods: {
    transform,
    touchStart(e) {
      this.x = e.clientX
      this.y = e.clientY
    },
    touchMove(e) {
      const {x, y} = this
      const touchMoveX = e.clientX //滑动变化坐标
      const touchMoveY = e.clientY //滑动变化坐标
      const angle = this.getAngle({x, y}, {x: touchMoveX, y: touchMoveY})
      if (Math.abs(angle) > 30) {
        return
      }
      //只能左滑
      this.isMoved = !(touchMoveX > x)
      if (this.isMoved && Math.abs(this.distance) <= this.initPanelMargin) {

        this.distance = touchMoveX - x
      }
    },
    touchEnd(e) {
      e = e.mp.changedTouches[0]
      const {x, y} = this
      const endX = e.clientX
      const distanceX = Math.abs(endX - x)
      if (this.isMoved) {
        if (distanceX > 30) {
          this.showBtnList = true
          this.distance = -this.initPanelMargin
        } else {
          this.showBtnList = false
          this.distance = 0
        }

      } else {
        this.showBtnList = false
        this.distance = 0
      }
    },
    getAngle(start, end) {
      const _X = end.x - start.x, _Y = end.y - start.y
      //返回角度 /Math.atan()返回数字的反正切值
      return 360 * Math.atan(_Y / _X) / (2 * Math.PI);
    }
  }
}
</script>
<style lang="scss">
.has-action-row {
  position: relative;
  transition: all 0.3s linear;

  .active-panel {
    position: absolute;
    left: 100%;
    top: 0;
    height: 100%;
    display: flex;
    > div {
      flex: 1;
      display: flex;
      align-items: center;
      justify-content: center;
      color: #FFFFFF;
      font-size: 26rpx;

      &.warning {
        background-color: red;
      }

      &.primary {
        background-color: #329fda;
      }

      &.text {
        background-color: #494949;
      }
      &:not(:last-child){
        border-right: 1px solid #FFFFFF;
      }
    }
  }
}
</style>

