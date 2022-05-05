<template>
  <div :class="{ 'main-app': true, 'menu-unfold': collapsed }">
    <div class="main-header">
      <a-button
        type="primary"
        style="margin-bottom: 16px"
        @click="toggleCollapsed"
      >
        <MenuUnfoldOutlined v-if="collapsed" />
        <MenuFoldOutlined v-else />
      </a-button>
      <div class="breadcrumb">
        <a-breadcrumb>
          <a-breadcrumb-item>首页</a-breadcrumb-item>
          <a-breadcrumb-item>
            <a href>统计</a>
          </a-breadcrumb-item>
        </a-breadcrumb>
      </div>
      <ul class="user-info">
        <li>欢迎</li>
        <li>退出</li>
      </ul>
    </div>
  </div>
</template>

<script>
import { reactive, watch, toRefs, emit } from "vue";
import {
  MenuFoldOutlined,
  MenuUnfoldOutlined,
} from "@ant-design/icons-vue";
export default {
  props: ["collapsed"],
  components: {
    MenuFoldOutlined,
    MenuUnfoldOutlined,
  },
  setup(props, ctx) {
    const state = reactive({
      preOpenKeys: ["sub1"],
    });

    watch(
      () => state.openKeys,
      (_val, oldVal) => {
        state.preOpenKeys = oldVal;
      }
    );
    const toggleCollapsed = () => {
      //props.collapsed = !props.collapsed;
      ctx.emit("update:collapsed", !props.collapsed);
      state.openKeys = state.collapsed ? [] : state.preOpenKeys;
    };
    return {
      toggleCollapsed,
      ...toRefs(state),
    };
  },
};
</script>

<style>
</style>