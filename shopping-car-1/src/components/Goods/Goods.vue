<template>
  <div class="goods-container">
    <!-- 左侧图片 -->
    <div class="thumb">
      <div class="custom-control custom-checkbox">
        <!-- 复选框 -->
        <input
          type="checkbox"
          class="custom-control-input"
          :id="'cb' + id"
          :checked="state"
          @change="stateChange"
        />
        <label class="custom-control-label" :for="'cb' + id">
          <!-- 商品的缩略图 -->
          <img src="../../assets/logo.png" alt="" />
        </label>
      </div>
    </div>
    <!-- 右侧信息区域 -->
    <div class="goods-info">
      <!-- 商品标题 -->
      <h6 class="goods-title">{{ title }}</h6>
      <div class="goods-info-bottom">
        <!-- 商品价格 -->
        <span class="goods-price">{{ price }}</span>
        <!-- 商品的数量 -->
        <Counter :num="count" :id="id"></Counter>
      </div>
    </div>
  </div>
</template>


<script>
import Counter from "@/components/Counter/Counter.vue";
export default {
  components: {
    Counter,
  },
  props: {
    title: {
      type: String,
      default: "",
    },
    price: {
      type: Number,
      default: 0,
    },
    id: {
      type: Number,
      required: true,
    },

    state: {
      type: Boolean,
      default: false,
    },

    count: {
      type: Number,
      require: true,
    },
  },

  methods: {
    stateChange(e) {
      console.log("----------stateChange----------------");
      console.log(e.target.checked);

      // 传递过去的数据应该是有id和state两个属性;
      // id确定是那个Goods， state确定状态 但是这个id如何得到了  傻逼了直接输入this.id即可
      //  console.log(this.id);
      // 封装传递过去的数据  {id:id, value:state}
      const state = e.target.checked;

      const obj = { id: this.id, value: state };

      // Goods子组件发送给App父组件
      this.$emit("state-change", obj);
    },
  },
};
</script>

<style lang="less" scoped>
.goods-container {
  + .goods-container {
    border-top: 1px solid #efefef;
  }
  padding: 10px;
  margin-bottom: 52px;
  display: flex;
  .thumb {
    display: flex;
    align-items: center;
    img {
      width: 100px;
      height: 100px;
      margin: 0 10px;
    }
  }

  .goods-info {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    flex: 1;
    .goods-title {
      font-weight: bold;
      font-size: 12px;
    }
    .goods-info-bottom {
      display: flex;
      justify-content: space-between;
      .goods-price {
        font-weight: bold;
        color: red;
        font-size: 13px;
      }
    }
  }
}
</style>
