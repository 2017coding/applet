<template>
  <view class="popup-components" v-show="value">
    <view :class="maskClass" @tap="handleClickMask" />
    <view class="popup-content" :class="classObj">
      <slot></slot>
    </view>
  </view>
</template>

<script>
export default {
  name: 'Popup',
  props: {
    // 是否打开弹窗
    value: {
      type: Boolean
    },
    // 是否开启动画
    animation: {
      type: Boolean,
      default: true
    },
    // 弹出方式
    type: {
      tyep: String, // top center bottom left right
      default: 'bottom'
    },
    // 蒙版点击是否关闭弹窗
    maskClick: {
      type: Boolean,
      default: true
    }
  },
  computed: {
    maskClass () {
      let str = ''
      if (this.animation) {
        if (this.value) {
          str = 'animation-mask-start'
        } else {
          str = 'animation-mask-end'
        }
      }
      return `mask ${str}`
    },
    classObj () {
      // return {
      //   animation: this.animation,
      //   type: this.type
      // }
      let str = ''
      if (this.animation) {
        if (this.value) {
          str = `animation-${this.type} animation-${this.type}-start`
        } else {
          str = `animation-${this.type} animation-${this.type}-end`
        }
      }
      return `${str} ${this.type}`
    }
  },
  methods: {
    handleClickMask () {
      if (!this.maskClick) return
      this.$emit('input', false)
    }
  }
}
</script>

<style lang="scss" scoped>
.popup-components{
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  .mask{
    position: absolute;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, .5);
    opacity: 0;
    transition: all .2s linear;
    &.animation-mask-start{
      opacity: 1;
    }
    &.animation-mask-end{
      opacity: 0;
    }
  }
  .popup-content{
    position: absolute;
    width: 100%;
    &.bottom{
      left: 0;
      right: 0;
      bottom: 0;
    }
    &.animation-bottom{
      bottom: -100%;
      transition: all .5s linear;
    }
    &.animation-bottom-start{
      bottom: 0;
    }
    &.animation-bottom-end{
      bottom: 0;
    }
    &.top{
      left: 0;
      right: 0;
      top: 0;
    }
    &.animation-top{
      top: -100%;
      transition: all .5s linear;
    }
    &.animation-top-start{
      top: 0;
    }
    &.animation-top-end{
      top: 0;
    }
    &.left{
      left: 0;
      top: 0;
      bottom: 0;
    }
    &.animation-left{
      left: -100%;
      transition: all .5s linear;
    }
    &.animation-left-start{
      left: 0;
    }
    &.animation-left-end{
      left: 0;
    }
    &.right{
      top: 0;
      right: 0;
      bottom: 0;
    }
    &.animation-right{
      right: -100%;
      transition: all .5s linear;
    }
    &.animation-right-start{
      right: 0;
    }
    &.animation-right-end{
      right: 0;
    }
  }
}
</style>
