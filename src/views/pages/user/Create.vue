<template>
  <div>
    <h1>{{id ? '编辑' : '新建'}}管理员</h1>
    <el-form label-width="130px" @submit.native.prevent="submit">
      <el-form-item label="用户名:">
        <el-input style="width: 200px;" type="text" placeholder="请输入内容" v-model="adminuser.username"></el-input>
      </el-form-item>

      <el-form-item label="用户密码:">
        <el-input style="width: 200px;" type="text" placeholder="请输入内容" v-model="adminuser.password"></el-input>
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
      adminuser: {}
    }
  },
  components: {

  },
  methods: {
    async submit() {
      let res
      if(this.adminuser !== ''){
        if(this.id){
        res = await this.$http.put(`rest/admin_user/${this.id}`, this.adminuser)
      }else{
        res = await this.$http.post('rest/admin_user', this.adminuser)
      }
      this.$router.push('/admin/user/list')
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
      const res = await this.$http.get(`rest/admin_user/${this.id}`)
      this.adminuser = res.data
    }
  },
  created(){
    this.id && this.fetch()
  }
}
</script>

<style scoped lang="css">

</style>
