<template>
  <div>
    <MyHeader title="购物车案例"></MyHeader>
    <div class="main">
      <MyGoods v-for="obj in list" :key="obj.id" :gObj="obj"></MyGoods>
    </div>
    <MyFooter @changeAll="allFn" :arr="list"></MyFooter>
  </div>
</template>

<script>
// 项目初始化
import MyHeader from "./components/MyHeader.vue";
import MyFooter from "./components/MyFooter.vue";
import MyGoods from "./components/MyGoods.vue";

export default {
  components: {
    MyHeader,
    MyFooter,
    MyGoods,
  },
  data() {
    return {
      list: [], // 商品所有数据
    };
  },
  created() {
    // 不必在自己引入axios变量, 而是直接使用全局属性$axios
    this.$axios({
      url: "/api/cart",
    }).then((res) => {
      console.log(res);
      this.list = res.data.list;
    });
  },
  methods: {
    allFn(bool) {
      this.list.forEach((obj) => (obj.goods_state = bool));
      // 把MyFooter内的全选状态true/false同步给所有小选框的关联属性上
    },
  },
};
</script>

<style scoped>
.main {
  padding-top: 45px;
  padding-bottom: 50px;
}
</style>