<template>
  <el-card>
      <bread-crumb slot="header">
        <template slot="title">账户信息</template>
      </bread-crumb>
      <el-form ref="myFrom" :model="formData" :rules="rules" style="margin-left:100px" label-width="100px">
          <el-form-item prop="name" label="用户名">
              <el-input v-model="formData.name" style="width:40%"></el-input>
          </el-form-item>
           <el-form-item prop="intro" label="简介">
               <el-input v-model="formData.intro" style="width:40%"></el-input>
           </el-form-item>
           <el-form-item prop="email" label="邮箱">
               <el-input v-model="formData.email" style="width:40%"></el-input>
           </el-form-item>
           <el-form-item prop="mobile" label="手机号">
               <el-input v-model="formData.mobile" disabled style="width:40%"></el-input>
           </el-form-item>
           <el-form-item>
               <el-button @click="saveUserInfo" type="primary">保存信息</el-button>
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
      defaultImg: require('../../assets/img/header.jpg'),
      rules: {
        name: [{ required: true, message: '用户名不能为空' }, {
          min: 3, max: 9, message: '用户名长度在3到9个字符之间'
        }],
        email: [{ required: true, message: '邮箱不能为空' }, {
          pattern: /^(\w-*\.*)+@(\w-?)+\.\w{2,}$/,
          message: '邮箱格式不正确'
        }]
      }
    }
  },
  methods: {
    getUserInfo () {
      this.$axios({
        url: '/user/profile'

      }).then(result => {
        this.formData = result.data
      })
    },
    saveUserInfo () {
      this.$refs.myFrom.validate().then(result => {
        this.$axios({
          url: '/user/profile',
          method: 'patch',
          data: this.formData
        }).then(result => {
          this.$message({
            type: 'success',
            message: '保存用户信息成功'
          })
        })
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
