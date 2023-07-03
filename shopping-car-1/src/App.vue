<template>
  <div id="app">
    <!-- 1.头部 -->
    <Header></Header>

    <!-- 2.商品详情 -->
    <Goods
      v-for="item in list"
      :key="item.id"
      :title="item.goods_name"
      :price="item.goods_price"
      :state="item.goods_state"
      :id="item.id"
      :count="item.goods_count"
      @state-change="getNewState"
    ></Goods>

    <!-- 3.尾部 -->
    <Footer
      :isfull="fullstate"
      :amount="amt"
      :all="countAll"
      @full-change="getFullState"
    ></Footer>
  </div>
</template>

/* 
日期：2023年7月1日
功能：重新写购物车案例 不看视频 自己做笔记操作 
*/


<script>
import Header from "@/components/Header/Header.vue";
import Footer from "@/components/Footer/Footer.vue";
import Goods from "@/components/Goods/Goods.vue";
import axios from "axios";

import bus from "@/components/eventBus.js";

export default {
  name: "App",

  data() {
    return {
      list: [
        {
          id: 1,
          goods_name: "秋季卫衣2023秋季款韩版上衣",
          goods_img: "../../assets/logo.png",
          goods_count: 1,
          goods_state: true,
          goods_price: 28,
        },
        {
          id: 2,
          goods_name: "秋季卫衣2023秋季款韩版上衣",
          goods_img: "../../assets/logo.png",
          goods_count: 1,
          goods_state: true,
          goods_price: 280,
        },
        {
          id: 3,
          goods_name: "秋季卫衣2023秋季款韩版上衣",
          goods_img: "../../assets/logo.png",
          goods_count: 1,
          goods_state: true,
          goods_price: 28,
        },
        {
          id: 4,
          goods_name: "秋季卫衣2023秋季款韩版上衣",
          goods_img: "../../assets/logo.png",
          goods_count: 1,
          goods_state: true,
          goods_price: 28,
        },
        {
          id: 5,
          goods_name: "秋季卫衣2023秋季款韩版上衣",
          goods_img: "../../assets/logo.png",
          goods_count: 1,
          goods_state: true,
          goods_price: 28,
        },
        {
          id: 6,
          goods_name: "秋季卫衣2023秋季款韩版上衣",
          goods_img: "../../assets/logo.png",
          goods_count: 1,
          goods_state: true,
          goods_price: 28,
        },
        {
          id: 7,
          goods_name: "秋季卫衣2023秋季款韩版上衣",
          goods_img: "../../assets/logo.png",
          goods_count: 1,
          goods_state: true,
          goods_price: 28,
        },
        {
          id: 8,
          goods_name: "秋季卫衣2023秋季款韩版上衣",
          goods_img: "../../assets/logo.png",
          goods_count: 1,
          goods_state: true,
          goods_price: 28,
        },
        {
          id: 9,
          goods_name: "秋季卫衣2023秋季款韩版上衣",
          goods_img: "../../assets/logo.png",
          goods_count: 1,
          goods_state: true,
          goods_price: 28,
        },
        {
          id: 10,
          goods_name: "秋季卫衣2023秋季款韩版上衣",
          goods_img: "../../assets/logo.png",
          goods_count: 1,
          goods_state: true,
          goods_price: 28,
        },
      ],
    };
  },

  // 计算属性
  computed: {
    fullstate() {
      return this.list.every((item) => item.goods_state);
    },

    amt() {
      return this.list
        .filter((item) => item.goods_state)
        .reduce(
          (total, item) => (total += item.goods_count * item.goods_price),
          0
        );
    },

    countAll() {
      return this.list
        .filter((item) => item.goods_state)
        .reduce((sum, item) => (sum += item.goods_count), 0);
    },
  },

  components: {
    Header,
    Goods,
    Footer,
  },

  methods: {
    async initCartList() {
      // 特码的 接口有问题  老是访问不了
      // const { data: res } = await axios.get(
      //   "https://applet-base-api-t.itheima.net/api/goods"
      // );
      // console.log(typeof res.data);
      // console.log(res.data.length);
      // this.list = res.data;
      // for (var i = 0; i < this.list.length; i++) {
      //   this.list[i].goods_count = 1;
      //   this.list[i].goods_state = true;
      // }

      console.log(this.list);
    },

    getNewState(e) {
      // 自己犹豫了一下是否要加参数  因为@state-change="stateChange"并没有添加参数 但是子组件是传递参数的
      console.log("接收子组件传递过来的数据");
      console.log(e);

      // 参数e的数据格式：{id:id, value:state}
      this.list.some((item) => {
        if (item.id === e.id) {
          item.goods_state = e.value;
          return true; // 这里的return true啥意思
        }
      });
    },

    getFullState(e) {
      console.log("接收到子组件传过来的数据：" + e);

      this.list.forEach((item) => {
        item.goods_state = e;
      });
    },
  },

  created() {
    this.initCartList();

    bus.$on("share", (e) => {
      console.log(e);

      this.list.some((item) => {
        if (item.id == e.id) {
          item.goods_count = e.value;
          return true;
        }
      });
    });
  },
};
</script>

<style lang="less">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
