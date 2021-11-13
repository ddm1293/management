<template>
  <div>
    <el-menu
        style="width: 200px; min-height: calc(100vh - 50px)"
        default-active="user"
        :default-openeds="[1]"
        class="el-menu-vertical-demo">
      <!--        @open="handleOpen"
              @close="handleClose"-->


      <el-sub-menu index="1">
        <template #title>系统管理</template>
        <el-menu-item index="user">用户管理</el-menu-item>
      </el-sub-menu>

      <el-menu-item index="data">数据管理</el-menu-item>

    </el-menu>
  </div>
</template>

<script>
export default {
  name: "Aside"
}
</script>

<style scoped>

</style>