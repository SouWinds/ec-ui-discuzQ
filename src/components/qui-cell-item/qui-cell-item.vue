<template>
  <view :class="['cell-item', { border: border }, classItem]" @tap="$_click">
    <view class="cell-item__body">
      <qui-icon
        class="leftIcon"
        :name="leftIcon"
        size="36"
        :color="iconColor"
        v-if="leftIcon"
        :style="{ background: iconBackgroundColor }"
      ></qui-icon>
      <view class="cell-item__body__left" v-if="slotLeft">
        <slot></slot>
      </view>
      <view class="cell-item__body__content fbh" @tap="contentClick">
        <view class="cell-item__body__content-title" v-if="title" v-text="title"></view>
        <view
          class="cell-item__body__content-brief identityAdmin"
          v-if="brief"
          v-text="brief"
        ></view>
      </view>
      <view class="cell-item__body__right" v-if="slotRight">
        <slot></slot>
        <qui-icon
          class="arrow"
          name="icon-folding-r"
          size="26"
          color="#ddd"
          v-if="arrow"
        ></qui-icon>
      </view>
      <view class="cell-item__body__right" v-if="!slotRight">
        <text class="cell-item__body__right-text">
          {{ addon }}
        </text>
        <qui-icon
          class="arrow"
          name="icon-folding-r"
          size="26"
          color="#ddd"
          v-if="arrow"
        ></qui-icon>
        <view class="cell-item__body__right-brief" v-if="briefRight">{{ briefRight }}</view>
      </view>
    </view>
    <view v-if="addon2" v-text="addon2" class="cell-item_children"></view>
  </view>
</template>

<script>
export default {
  name: 'QuiCellItem',

  props: {
    title: {
      type: String,
      default: '',
    },
    brief: {
      type: String,
      default: '',
    },
    addon: {
      type: String,
      default: '',
    },
    arrow: {
      type: Boolean,
      default: false,
    },
    addon2: {
      type: String,
      default: '',
    },
    briefRight: {
      type: String,
      default: '',
    },
    border: {
      type: Boolean,
      default: true,
    },
    disabled: {
      type: Boolean,
      default: false,
    },
    slotLeft: {
      type: Boolean,
      default: false,
    },
    slotRight: {
      type: Boolean,
      default: false,
    },
    classItem: {
      type: String,
      default: '',
    },
    // 左侧图标
    leftIcon: {
      type: String,
      default: '',
    },
    iconColor: {
      type: String,
      default: '',
    },
    iconBackgroundColor: {
      type: String,
      default: '',
    },
  },

  methods: {
    /**
     * item项点击事件
     */
    $_click(e) {
      if (!this.disabled) {
        this.$emit('click', e);
      }
    },
    contentClick(e) {
      if (!this.disabled) {
        this.$emit('contentClick', e);
      }
    },
  },
};
</script>

<style lang="scss">
@import '@/styles/base/variable/global.scss';
@import '@/styles/base/theme/fn.scss';
.cell-item {
  position: relative;
  padding-left: 20rpx;
}
.cell-item.border {
  // border-bottom: 2rpx solid --color(--qui-BOR-ED);
  // transition: $switch-theme-time;
}

.cell-item__body {
  position: relative;
  display: flex;
  height: 100rpx;
  align-items: center;
  justify-content: space-between;
  box-sizing: border-box;
}

.cell-item__body__content-title {
  font-size: $fg-f28;
  color: --color(--qui-FC-333);
  transition: $switch-theme-time;
}

.cell-item__body__content-brief,
.cell-item__body__right-brief {
  // margin-top: 6rpx;
  font-size: $fg-f20;
  color: --color(--qui-FC-AAA);
}

.cell-item__body__content {
  flex: 1 1 0%;
}

.cell-item__body__right {
  align-items: center;
  justify-content: flex-end;
  font-size: $fg-f28;
  text-align: right;
}

.cell-item__body__right .cell-item__body__right-text {
  font-size: $fg-f28;
  word-break: break-all;
}

.cell-item__children {
  padding: 20upx 0;
  margin: 0 20upx;
}

.arrow {
  margin-left: 20rpx;
}
.leftIcon {
  margin-right: 20rpx;
  padding: 20rpx;
  border-radius: 100rpx;
  background-blend-mode: overlay, hard-light, normal;
}
.identityAdmin {
  height: 18px;
  line-height: 18px;
  align-items: center;
  background: #fff !important;
  border: #ccc 1px solid;
  border-radius: 10px;
  font-size: 14px;
  margin-left: -14rpx;
  margin-top: -10rpx;
  padding: 6rpx 14rpx;
  transform: scale(0.5);
}
</style>
