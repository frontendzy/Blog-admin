<template>
  <div>
    <h1>{{id ? '编辑' : '新建'}}分类</h1>
    <el-form label-width="130px" @submit.native.prevent="submit">
      <el-form-item label="分类名称:">
        <el-input style="width: 200px;" type="text" placeholder="请输入内容" v-model="classdata.name" maxlength="10" show-word-limit></el-input>
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
      classdata: {}
    }
  },
  components: {

  },
  methods: {
    async submit() {
      let res
      if(this.model !== ''){
        if(this.id){
        res = await this.$http.put(`rest/classification/${this.id}`, this.classdata)
      }else{
        res = await this.$http.post('rest/classification', this.classdata)
      }
      this.$router.push('/admin/classification/list')
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
      const res = await this.$http.get(`rest/classification/${this.id}`)
      this.classdata = res.data
    }
  },
  created(){
    this.id && this.fetch()
  }
}
</script>

<style scoped lang="css">

</style>
