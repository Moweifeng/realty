<template>
  <!-- 商品数量box子组件-->
  <div class="goodsNumber">
    购买数量:
    <div class="mui-numbox" data-numbox-min="1">
      <button class="mui-btn mui-btn-numbox-minus" type="button">-</button>
      <input
        id="test"
        class="mui-input-numbox"
        type="number"
        @change="numberChange"
        ref="numberBox"
      />
      <button class="mui-btn mui-btn-numbox-plus" type="button">+</button>
    </div>
  </div>
</template>
<script>
import mui from '../../lib/mui-master/dist/js/mui.min.js'
export default {
    mounted() {
        // mui-numbox失效。因为要等页面渲染好才能执行相应的代码。所以要等页面渲染完成后再执行nui-numbox里的动画
        mui(".mui-numbox").numbox();//初始化
    },
    methods: {
        numberChange() {
            let number = this.$refs.numberBox.value;
            this.$emit('fuc',number)
        }
    },
    // 商品库存这项数据是由axios请求的，设置商品最大值的时候需要依赖此数据。
    // 设置最大值的时候axios请求的数据还没到,所以maxgoods==undefine。
    // 可以通过watch方式监听数据的变化来解决
    props:['maxgoods'],
    watch:{
        // 通过mui里的js API来控制最大值
        maxgoods(newVal,oldVal) {
            mui(".mui-numbox").numbox().setOption('max',newVal)
        }
    }

}
</script>
<style lang="less" scoped>
.goodsNumber {
  margin-bottom: 10px;
}
</style>