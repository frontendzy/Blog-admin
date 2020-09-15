<template>
  <div>
    <el-breadcrumb separator="/" style="margin-bottom: 15px">
      <el-breadcrumb-item :to="{ path: '/admin/classification/create' }">分类编辑</el-breadcrumb-item>
      <el-breadcrumb-item :to="{ path: '/admin/classification/list' }">分类列表</el-breadcrumb-item>
    </el-breadcrumb>

    <el-card class="box-card" style="box-shadow: 0 1px 1px rgba(0, 0, 0, 0.15)">
      <router-view></router-view>
    </el-card>
  </div>
</template>