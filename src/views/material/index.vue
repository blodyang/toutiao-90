<template>
  <el-card  v-loading="loading" element-loading-text="拼命加载中">
    <!-- 头部 -->
      <bread-crumb slot="header">
        <template slot="title">
            素材管理
        </template>
      </bread-crumb>
         <el-tabs v-model="activeName" @tab-click='changeTab'>
          <!-- 标签 -->
          <el-tab-pane label="全部图片" name="all">
            <div class="img-list">
              <el-card class="img-card" v-for="item in list" :key="item.id">
                <img :src="item.url" alt="">
                <el-row  class="operate" align="middle" type="flex" justify="space-around">
                  <i class="el-icon-star-on"></i>
                  <i class="el-icon-delete"></i>
                </el-row>
              </el-card>
            </div>
          </el-tab-pane>
          <el-tab-pane label="收藏图片" name="collect">
            <div class="img-list">
              <el-card class="img-card" v-for="item in list" :key="item.id">
                <img :src="item.url" alt="">
              </el-card>
            </div>
          </el-tab-pane>
      </el-tabs>
      <el-row type="flex" justify="center">
                    <el-pagination background layout="prev, pager, next"
                                :current-page="page.currentPage"
                                :page-size="page.pageSize"
                                :total="page.total"
                                @current-change="changePage">
                    </el-pagination>

            </el-row>
  </el-card>
</template>

<script>
export default {
  data () {
    return {
      activeName: 'all',
      list: [],
      page: {
        currentPage: 1,
        pageSize: 8,
        total: 0
      }
    }
  },
  methods: {
    changePage (newPage) {
      this.page.currentPage = newPage
      this.getMaterial()
    },
    changeTab () {
      this.page.currentPage = 1
      this.getMaterial()
    },
    getMaterial () {
      this.loading = true
      this.$axios({
        url: '/user/images',
        params: {
          page: this.page.currentPage,
          per_page: this.page.pageSize,
          collect: this.activeName === 'collect'
        }
      }).then(result => {
        this.list = result.data.results
        this.page.total = result.data.total_count
        this.loading = false
      })
    }
  },
  created () {
    this.getMaterial()
  }

}
</script>

<style lang="less" scoped>
  .img-list{
    display: flex;
    flex-wrap: wrap;
    .img-card{
      width:200px;
      height: 220px;
      margin: 20px 50px;
      position: relative;
      img{
        width: 100%;
        height: 100%;
      }
      .operate{
        width: 100%;
        position:absolute;
        left: 0;
        bottom: 0;
        font-size: 22px;
        height: 40px;
        background-color: #f4f5f6;
      }
    }
  }
</style>
