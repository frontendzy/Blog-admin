<template>
  <div>
    <h1>{{id ? '编辑' : '新建'}}文章</h1>
    <el-form label-width="130px" @submit.native.prevent="submit">
        <el-row>
          <el-col :span="12">
            <div class="grid-content bg-purple-dark">
              <el-form-item label="文章标题:">
                <el-input style="width: 200px;" type="text" placeholder="请输入内容" v-model="article.title"></el-input>
              </el-form-item>
            </div>
          </el-col>
          <el-col :span="12">
            <div class="grid-content bg-purple-dark">
              <el-form-item label="分类:">
                <el-select v-model="article.belong" placeholder="请选择">
                  <el-option 
                            v-for="item in belongs" 
                            :key="item._id" 
                            :label="item.name" 
                            :value="item._id"></el-option>
                </el-select>
              </el-form-item>
            </div>
          </el-col>
        </el-row>

      <el-form-item label="描述:">
        <el-input type="textarea" autosize placeholder="请输入内容" v-model="article.description"></el-input>
      </el-form-item>

      <el-form-item label="背景:">
        <el-upload
          class="avatar-uploader"
          :action="uploadUrl"
          :headers="getAuthHeaders()"
          :show-file-list="false"
          :on-success="afterUpload">
          <img v-if="article.image" :src="article.image" class="avatar">
          <i v-else class="el-icon-plus avatar-uploader-icon"></i>
        </el-upload>
      </el-form-item>

      <el-form-item label="内容:">
        <mavon-editor v-model="article.body" @imgAdd="$imgAdd" ref="md"/>
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
      article: {},
      belongs: {}
    }
  },
  methods: {
    //获取文章信息
    async fetch_article(){
      const res = await this.$http.get(`rest/article/${this.id}`)
      this.article = res.data
    },
    async fetch_belongs() {
      const res = await this.$http.get('rest/classification')
      this.belongs = res.data
    },
    afterUpload(res) {
      this.$set(this.article, 'image', res.url)
    },
    async $imgAdd(pos, $file){
        // 第一步.将图片上传到服务器.
       const formdata = new FormData();
       formdata.append('file', $file);
       //网络请求
       const res = await this.$http.post('upload', formdata)
       // console.log(res);
       this.$refs.md.$img2Url(pos, res.data.url);
    },
    async submit() {
      let res
      if(this.article !== ''){
        if(this.id){
        res = await this.$http.put(`rest/article/${this.id}`, this.article)
      }else{
        res = await this.$http.post('rest/article', this.article)
      }
      this.$router.push('/admin/article/list')
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
  },
  created() {
    this.id && this.fetch_article();
    this.fetch_belongs()
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
