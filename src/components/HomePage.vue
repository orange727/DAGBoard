<template>
  <div class="page-content">
    <div class="tapBar">
      <div class="profile">你好，刘火昆</div>
      <div :class="item.sel ? 'tapEachSel ': 'tapEach'"
        @click="selStep(i)"
        v-for="(item , i) in menu" :key="i">{{ item.name }}</div>
    </div>
    <div class="mainContent">
      <NODE v-if="menu[0].sel"/>
      <DAG v-if="menu[1].sel"/>
    </div>
  </div>
</template>

<script>
import { menu } from "./DataMainPage.js";
import NODE from "./NodePage";
import DAG from "./DagPage";

export default {
  data() {
    return {
      menu: menu
    };
  },
  methods: {
    selStep(i) {
      window.sessionStorage["menu"] = i;
      this.menu.forEach((item, n) => {
        i - n === 0 ? (item.sel = true) : (item.sel = false);
      });
      this.menu = JSON.parse(JSON.stringify(this.menu));
    }
  },
  mounted() {
    if (window.sessionStorage["menu"]) {
      const i = window.sessionStorage.menu;
      this.selStep(i);
    }
  },
  components: {
    DAG,
    NODE
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.page-content {
  position: absolute;
  left: 0;
  top: 0;
  right: 0;
  bottom: 0;
  overflow: hidden;
}
.profile {
  font-size: 12px;
  line-height: 60px;
  color: #fff;
  margin-right: 60px;
}
.tapBar {
  width: 100%;
  height: 60px;
  background-color: #212528;
  display: flex;
  padding-top: 10px;
  padding-left: 40px;
}
.tapEach {
  height: 50px;
  line-height: 50px;
  text-align: center;
  width: 100px;
  color: #ffffff;
  cursor: pointer;
}
.tapEachSel {
  height: 50px;
  line-height: 50px;
  text-align: center;
  width: 100px;
  color: #212528;
  background: #cccccc;
  cursor: pointer;
  box-sizing: border-box;
}
.mainContent {
  width: 100%;
  position: absolute;
  left: 0;
  top: 60px;
  bottom: 0;
  text-align: left;
}
</style>
