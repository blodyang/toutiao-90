<template>
<el-container>
  <el-aside style="min-height:100vh;background-color:#353b4e;width:220px">
    <layout-aside></layout-aside>
  </el-aside>
  <el-container>
    <el-header>
      <layout-header></layout-header>
    </el-header>
    <el-main>主要区域</el-main>
  </el-container>
</el-container>
</template>

<script>
import layoutAside from '../../components/layout-aside'
import layoutHeader from '../../components/layout-header'
export default {
  components: {
    'layout-aside': layoutAside,
    'layout-header': layoutHeader
  }
}
</script>

<style>

</style>
