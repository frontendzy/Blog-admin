<template>
  <div>
    <h1>分类列表</h1>
    <el-table :data="data" style="width: 100%">
    <el-table-column prop="_id" label="ID"></el-table-column>
    <el-table-column prop="title" label="标题"></el-table-column>
    <el-table-column prop="belong.name" label="分类"></el-table-column>
     <el-table-column fixed="right" label="操作" width="200">
      <template slot-scope="scope">
        <el-button @click="$router.push(`/admin/article/edit/${scope.row._id}`)" size="small" type="primary">编辑</el-button>
        <el-button @click="remove(scope.row)" size="small" type="danger">删除</el-button>
      </template>
    </el-table-column>
  </el-table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      data: []
    }
  },
  methods: {
    async fetch() {
      const res = await this.$http.get('rest/article');
      this.data = res.data;
    },
    async remove(row) {
      this.$confirm('此操作将永久删除该分类, 是否继续?', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        })
        .then(async () => {
          const res = await this.$http.delete(`rest/article/${row._id}`)
          this.$message({
            type: 'success',
            message: '删除成功!'
          });
          this.fetch();
        })
    }
  },
  created() {
    this.fetch();
  }
}
</script>

<style scoped lang="css">

</style>
