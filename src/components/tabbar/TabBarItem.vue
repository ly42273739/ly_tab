<template>
  <div class="tab-bar-item" @click="itemClick">
    <div v-if="!isActive">
      <slot name="item-icon"></slot>
    </div>
    <div v-else>
      <slot name="item-icon-active"></slot>
    </div>

    <!-- 这里不能在插槽里面直接绑定样式，根据插槽的定义，会被直接替换掉整个，所以绑定的样式等于没有 -->
    <!-- 解决方法：在外面包一层div -->
    <div :style="activeStyle">
      <slot name="item-text"></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "TabBarItem",
  props: {
    path: String,
    activecolor: {
      type: String,
      default: "red"
    }
  },
  data() {
    return {
      // isActive: false
    };
  },
  methods: {
    itemClick() {
      this.$router.replace(this.path);
    }
  },
  computed: {
    isActive() {
      // $route是当前活跃的组件路由
      //拿到当前活跃的组建路由判断当中是否包含当前的路由路径
      return this.$route.path.indexOf(this.path) !== -1;
    },
    activeStyle() {
      return this.isActive ? { color: this.activecolor } : {};
    }
  }
};
</script>

<style scoped>
.tab-bar-item {
  flex: 1;
  text-align: center;
  height: 49px;
}
</style>
