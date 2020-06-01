<template>
  <el-card  v-loading="loading" element-loading-text="拼命加载中">
      <bread-crumb slot="header">
        <template slot="title">
            评论管理
        </template>
      </bread-crumb>
      <!-- 表格 -->
      <el-table :data="list">
          <el-table-column prop="title" width="500" label="标题"></el-table-column>
          <el-table-column :formatter="formatterBoolean" prop="comment_status" label="评论状态"></el-table-column>
          <el-table-column prop="total_comment_count" label="总评论数"></el-table-column>
          <el-table-column prop="fans_comment_count" label="粉丝评论数"></el-table-column>
          <el-table-column label="操作">
              <template slot-scope="obj">

                <el-button size="small" type="text">修改</el-button>
                <el-button @click="openOrCloseState(obj.row)" size="small" type="text">
                    {{ obj.row.comment_status ? '关闭评论' : '打开评论'}}
                </el-button>
            </template>
          </el-table-column>
      </el-table>
      <el-row type='flex' justify="center" align="middle" style="height:80px">
      <!-- 分页组件 total 总页码  每页多少条-->
      <el-pagination background layout="prev, pager, next"
       :current-page="page.currentPage"
       :page-size="page.pageSize"
       :total="page.total"
       @current-change="changePage"
       ></el-pagination>
    </el-row>
  </el-card>
</template>

<script>
export default {
  data () {
    return {
      list: [],
      loading: false,
      page: {
        total: 0,
        pageSize: 10,
        currentPage: 1
      }
    }
  },
  methods: {
    changePage (newPage) {
      this.page.currentPage = newPage
      this.getComment()
    },
    getComment () {
      this.loading = true
      this.$axios({
        url: 'articles',
        params: { response_type: 'comment', page: this.page.currentPage, per_page: this.page.pageSize }
      }).then(result => {
        this.list = result.data.results
        this.page.total = result.data.total_count
        this.loading = false
      })
    },
    formatterBoolean (row, column, cellValue, index) {
      return cellValue ? '正常' : '关闭'
    },
    openOrCloseState (row) {
      const mess = row.comment_status ? '关闭评论将清除所有评论，读者也不能再进行评论，是否进行此操作?' : '此操作将开启评论，是否进行此操作?'
      this.$confirm(`${mess}`, '提示', {

      }).then(() => {
        this.$axios({
          method: 'put',
          url: '/comments/status',
          params: { article_id: row.id.toString() },
          data: { allow_comment: !row.comment_status } // 因为当前如果是打开 ,就要关闭 如果是关闭 就要打开
        }).then(result => {
          //  表示执行成功
          this.getComment() // 重新拉取评论管理数据
        })
      })
    }
  },
  created () {
    this.getComment()
  }
}
</script>

<style>

</style>
