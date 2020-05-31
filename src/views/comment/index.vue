<template>
  <el-card>
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
                <el-button size="small" type="text"> {{ obj.row.comment_status ? '关闭评论' : '打开评论'}}</el-button>
            </template>
          </el-table-column>
      </el-table>
  </el-card>
</template>

<script>
export default {
  data () {
    return {
      list: []
    }
  },
  methods: {
    getComment () {
      this.$axios({
        url: 'articles',
        params: { response_type: 'comment' }
      }).then(result => {
        this.list = result.data.results
      })
    },
    formatterBoolean (row, column, cellValue, index) {
      return cellValue ? '正常' : '关闭'
    }
  },
  created () {
    this.getComment()
  }
}
</script>

<style>

</style>
