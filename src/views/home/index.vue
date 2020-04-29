<template>
<el-container>
  <el-aside style="min-height:100vh;background-color:#353b4e;width:220px">
    <layout-aside></layout-aside>
  </el-aside>
  <el-container>
    <el-header>
      头部
    </el-header>
    <el-main>主要区域</el-main>
  </el-container>
</el-container>
</template>

<script>
import layoutAside from '../../components/layout-aside'
export default {
  components: {
    'layout-aside': layoutAside
  }
}
</script>

<style>

</style>
