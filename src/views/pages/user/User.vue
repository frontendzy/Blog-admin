<template>
  <div>
    <el-breadcrumb separator="/" style="margin-bottom: 15px">
      <el-breadcrumb-item :to="{ path: '/admin/user/create' }">管理员编辑</el-breadcrumb-item>
      <el-breadcrumb-item :to="{ path: '/admin/user/list' }">管理员列表</el-breadcrumb-item>
    </el-breadcrumb>

    <el-card class="box-card" style="box-shadow: 0 1px 1px rgba(0, 0, 0, 0.15)">
      <router-view></router-view>
    </el-card>
  </div>
</template>