<template>
  <div class="home">
    <Menu :collapsed="collapsed"/>
    <!-- <sliderNav :collapsed="collapsed" @collapsedFromSlide='handleReport'/> -->
    <div>
    <sliderNav v-model:collapsed="collapsed" /> 
    
    <router-view></router-view>
    </div>
    
  </div>
</template>

<script >
import Menu from "./components/menu.vue";
import sliderNav from "./components/sliderNav.vue";
import { reactive, toRefs } from "vue";
export default {
  components: {
    Menu,
    sliderNav,
  },
  setup() {
    const state = reactive({
      collapsed: false,
    });
    // const handleReport=(arg)=>{
    //   state.collapsed=arg
    // }
    return {
      // handleReport,
      ...toRefs(state),
    };
  },
};
</script>

<style lang='less'>
@import url("~@/assets/css/home.less");
</style>
