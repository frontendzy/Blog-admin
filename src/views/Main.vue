<template>
  <div>
    <el-container style="height: 100vh;">
      <el-aside width="200px" style="background-color: rgb(238, 241, 246)">
        <el-menu router :default-openeds="['1']" :default-active="$route.path">
            <el-menu-item-group>
              <el-menu-item index="/admin"><i class="el-icon-message"></i>首页</el-menu-item>
              <el-menu-item index="/admin/classification/list"><i class="el-icon-collection-tag"></i>分类</el-menu-item>
              <el-menu-item index="/admin/article/list"><i class="el-icon-document"></i>文章</el-menu-item>
              <el-menu-item index="/admin/user/list"><i class="el-icon-user-solid"></i>管理员</el-menu-item>
              <el-menu-item index="/admin/blogicon/create"><i class="el-icon-s-home"></i>Blog设置</el-menu-item>
              <el-menu-item index="/admin">评论</el-menu-item>
            </el-menu-item-group>
        </el-menu>
        <el-button @click="exitadmin" class="btn"><i class="el-icon-error"></i>退出</el-button>
      </el-aside>
        <el-main>
          <router-view></router-view>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script>
export default {
  name: 'Main',
  data() {
    return {

    }
  },
  methods: {
    exitadmin() {
      localStorage.clear();
      this.$router.push('/login')
      this.$message({
          type: 'success',
          message: '退出成功'
        })
    }
  }
}
</script>

<style scoped lang="css">
  .btn {
    width: 200px;
  }
</style>
