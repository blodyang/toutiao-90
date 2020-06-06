<template>
  <div class="cover-image">
      <div @click="OpneDialog" v-for="(item,index) in list" :key="index" class="cover-image-item">
          <img :src="item ? item :defaultImg" alt="">
      </div>
      <el-dialog :visible="dialogVisible" @close="closeDialog" title="选择封面图片"></el-dialog>
  </div>
</template>

<script>
export default {
  props: ['list'],
  data () {
    return {
      defaultImg: require('../../assets/img/pic_bg.png'),
      dialogVisible: false
    }
  },
  methods: {
    OpneDialog () {
      this.dialogVisible = true// 打开弹层
    },
    closeDialog () {
      this.dialogVisible = false// 关闭弹层
    }
  }

}
</script>

<style lang="less" scoped>
.cover-image{
    margin: 20px 100px;
    display: flex;
    .cover-image-item{
        border: 1px solid #ccc;
        width: 200px;
        height: 250px;
        padding: 10px;
    }
}
</style>
