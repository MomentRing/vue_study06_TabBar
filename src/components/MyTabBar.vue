<template>
  <div class="my-tab-bar">
    <div
      class="tab-item"
      v-for="(obj, index) in arr"
      :key="index"
      @click="btn(index, obj)"
      :class="{ current: selIndex === index }"
    >
      <!-- 图标 -->
      <span class="iconfont" :class="obj.iconText"></span>
      <!-- 文字 -->
      <span>{{ obj.text }}</span>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selIndex: 0,
    }
  },
  props: {
    arr: {
      type: Array,
      required: true,
      // 自定义校验规则
      validator(val) {
        if (val.length > 2 && val.length <= 5) {
          return true
        } else {
          console.log('数据需要2到5个')
          return false
        }
      },
    },
  },
  methods: {
    btn(ind, obj) {
      this.selIndex = ind
      this.$emit('changeCom', obj.componentName)
    },
  },
}
</script>

<style lang="less" scoped>
.my-tab-bar {
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  height: 50px;
  border-top: 1px solid #ccc;
  display: flex;
  justify-content: space-around;
  align-items: center;
  background-color: white;
  .tab-item {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
}

.current {
  color: #1d7bff;
}
</style>
