<template>
  <el-card>
      <bread-crumb slot="header">
        <template slot="title">账户信息</template>
      </bread-crumb>
      <el-form style="margin-left:100px" label-width="100px">
          <el-form-item label="用户名">
              <el-input v-model="formData.name" style="width:40%"></el-input>
          </el-form-item>
           <el-form-item label="简介">
               <el-input v-model="formData.intro" style="width:40%"></el-input>
           </el-form-item>
           <el-form-item label="邮箱">
               <el-input v-model="formData.email" style="width:40%"></el-input>
           </el-form-item>
           <el-form-item label="手机号">
               <el-input v-model="formData.mobile" disabled style="width:40%"></el-input>
           </el-form-item>
           <el-form-item>
               <el-button type="primary">保存信息</el-button>
           </el-form-item>
      </el-form>
      <el-upload class='head-upload' action="" :show-file-list="false">
          <img :src="formData.photo ? formData.photo : defaultImg" alt="">
      </el-upload>
  </el-card>
</template>

<script>
export default {
  data () {
    return {
      formData: {
        name: '',
        intro: '',
        photo: '',
        email: '',
        mobile: ''
      },
      defaultImg: require('../../assets/img/header.jpg')
    }
  },
  methods: {
    getUserInfo () {
      this.$axios({
        url: '/user/profile'

      }).then(result => {
        this.formData = result.data
      })
    }
  },
  created () {
    this.getUserInfo()
  }
}
</script>

<style lang="less" scoped>
    .head-upload {
   position: absolute;
   right: 300px;
   top:200px;
    img {
       width: 200px;
       height: 200px;
        border-radius: 50%;
    }
}
</style>
