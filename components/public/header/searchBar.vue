<template>
  <div class="search-panel">
    <el-row class="m-header-searchbar">
      <el-col :span="3" class="left">
        <img src="//s0.meituan.net/bs/fe-web-meituan/e5eeaef/img/logo.png" alt="美团" />
      </el-col>
      <el-col :span="15"
        class="center">
        <div class="wrapper">
            <el-input
            v-model="searchText"
            @focus="searchInputFocus"
            @blur="searchInputBlur"
            @input="searchInputInput"
            placeholder="搜索商家或地点"/>
          <button class="el-button el-button--primary"><i class="el-icon-search"/></button>
          <dl class="hotPlace" v-if="hotPlace">
              <dt>光标聚焦内容为空</dt>
              <dd v-for="(txt,index) in hotPlaceList" :key="index">{{txt}}</dd>
          </dl>
          <dl class="searchList" v-if="searchPlace">
              <dd>光标聚焦内容不为空</dd>
              <dd v-for="(txt,index) in searchPlaceList" :key="index">{{txt}}</dd>
          </dl>
        </div>
        <p class="suggset">
            <a href="#">故宫博物院</a>
            <a href="#">故宫博物院</a>
            <a href="#">故宫博物院</a>
            <a href="#">故宫博物院</a>
            <a href="#">故宫博物院</a>
        </p>
        <ul class="nav">
          <li><nuxt-link
            to="/"
            class="takeout">美团外卖</nuxt-link></li>
          <li><nuxt-link
            to="/"
            class="movie">猫眼电影</nuxt-link></li>
          <li><nuxt-link
            to="/"
            class="hotel">美团酒店</nuxt-link></li>
          <li><nuxt-link
            to="/"
            class="apartment">民宿/公寓</nuxt-link></li>
          <li><nuxt-link
            to="/"
            class="business">商家入驻</nuxt-link></li>
        </ul>
    </el-col>
      <el-col
        :span="6"
        class="right">
        <ul class="security">
          <li><i class="refund"/><p class="txt">随时退</p></li>
          <li><i class="single"/><p class="txt">不满意免单</p></li>
          <li><i class="overdue"/><p class="txt">过期退</p></li>
        </ul>
      </el-col>
    </el-row>
  </div>
</template>

<script>
export default {
  data(){
    return {
      searchText:"",
      isFoucs:false,
      hotPlaceList:["推荐搜索","推荐搜索","推荐搜索"],
      searchPlaceList:["推荐搜索","推荐搜索","推荐搜索"]
    }
  },
  computed:{
    hotPlace(){
      return this.isFoucs&&!this.searchText
    },
    searchPlace(){
      return this.isFoucs&&this.searchText
    },
  },
  methods:{
    searchInputFocus(){
      this.isFoucs = true
    },
    searchInputBlur(){
      setTimeout(()=>{
        this.isFoucs = false;
      },300)
      
    },
    searchInputInput(value){
      console.log("input")
    },

  }
};
</script>

<style lang="scss" scoped>
</style>