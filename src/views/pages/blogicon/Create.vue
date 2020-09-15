<template>
      <div>
        <el-form label-width="130px" @submit.native.prevent="submit">
          <el-form-item label="名称">
            <el-input v-model="data.name" style="width: 200px;"></el-input>
          </el-form-item>
          <el-form-item label="icon">
            <el-input v-model="data.iconclass" style="width: 200px;"></el-input>
          </el-form-item>
          <el-form-item label="link">
            <el-input v-model="data.link"></el-input>
          </el-form-item>
          <el-form-item>
            <el-button type="primary" native-type="submit">保存</el-button>
          </el-form-item>
        </el-form>
      </div>
</template>

<script>
export default {
  props: {
    id: {}
  },
  data() {
    return {
      data: {}
    }
  },
  components: {

  },
  methods: {
    async submit() {
      let res
      if(this.data !== ''){
        if(this.id){
        res = await this.$http.put(`rest/blog_icon/${this.id}`, this.data)
      }else{
        res = await this.$http.post('rest/blog_icon', this.data)
      }
      this.$router.push('/admin/blogicon/list')
        this.$message({
          type: 'success',
          message: '提交成功'
        })
      }else{
        this.$message({
          type: 'error',
          message: '提交失败'
        })
      }
    },
    async fetch(){
     const res = await this.$http.get(`rest/blog_icon/${this.id}`)
      this.data = res.data
    }
  },
  created() {
    this.id && this.fetch()
  }
}
</script>

<style scoped lang="css">
   .avatar-uploader .el-upload {
    border: 1px dashed #d9d9d9;
    border-radius: 6px;
    cursor: pointer;
    position: relative;
    overflow: hidden;
  }
  .avatar-uploader .el-upload:hover {
    border-color: #409EFF;
  }
  .avatar-uploader-icon {
    font-size: 28px;
    color: #8c939d;
    width: 178px;
    height: 178px;
    line-height: 178px;
    text-align: center;
  }
  .avatar {
    width: 178px;
    height: 178px;
    display: block;
  }
</style>
