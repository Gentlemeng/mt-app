<template>
  <el-container class="layout-default">
    <el-header height="auto">
      <my-header></my-header>
    </el-header>
    <el-main>
      <nuxt/>
    </el-main>
    <el-footer height="auto">
      <my-footer></my-footer>
    </el-footer>
</el-container>
</template>
<script>
import myHeader from './../components/public/header/index.vue'
import myFooter from './../components/public/footer/index'
export default {
  components:{
    myHeader,
    myFooter
  }
}
</script>

