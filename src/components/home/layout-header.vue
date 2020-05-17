<template>
<el-row type="flex" align="middle" class="layout-header">
    <el-col class="left" :span="12">
        <i class="el-icon-s-fold"></i>
        <span>江苏传智播客教育科技股份有限公司</span>
    </el-col>
    <el-col :span="12">
        <el-row class="right" type="flex" justify="end" align="middle">
            <img :src="!userInfo.photo ? userInfo.photo :defaultImg" alt="">
            <el-dropdown>
                <span>{{userInfo.name}}</span>
                <el-dropdown-menu slot="dropdown">
                    <el-dropdown-item>个人信息</el-dropdown-item>
                    <el-dropdown-item>git地址</el-dropdown-item>
                    <el-dropdown-item>退出登录</el-dropdown-item>
                </el-dropdown-menu>
            </el-dropdown>
        </el-row>
    </el-col>
</el-row>
</template>

<script>
export default {
  data () {
    return {
      userInfo: {},
      defaultImg: require('../../assets/img/header.jpg')
    }
  },
  created () {
    const token = localStorage.getItem('user-token')

    this.$axios({
      url: '/user/profile',
      headers: {
        Authorization: `Bearer ${token}`
      }
    }).then(result => {
      this.userInfo = result.data.data
    })
  }
}
</script>

<style lang="less" scoped>
.layout-header{
    .left{
        font-size: 20px;
        span{
            color:#2c3e50;
            font-size: 16px;
            margin-left: 5px;
        }
    }
    .right{
        img{
            width: 40px;
            border-radius: 50%;
            margin-right: 5px;
        }
    }
}
</style>
