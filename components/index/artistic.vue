<template>
  <section class="m-istyle">
    <dl>
      <dt>有格调</dt>
      <dd
        :class="{active:curIndex===index}"
        v-for="(category,index) in artistCategory"
        :key="index"
        :kind="category.kind"
        :keyword="category.keyword"
        @mouseover="over(index)"
      >{{category.name}}</dd>
    </dl>
    <ul class="ibody">
      <li v-for="item in cur" :key="item.title">
        <el-card :body-style="{ padding: '0px' }" shadow="never">
          <img :src="item.img" class="image" />
          <ul class="cbody">
            <li class="title">{{ item.title }}</li>
            <li class="pos">
              <span>{{ item.pos }}</span>
            </li>
            <li class="price">
              ￥
              <em>{{ item.price }}</em>
              <span>/起</span>
            </li>
          </ul>
        </el-card>
      </li>
    </ul>
  </section>
</template>

<script>
export default {
  data() {
    return {
      curIndex: 0,
      artistCategory: [
        {
          name: "全部",
          keyword: "景点",
          kind: "all"
        },
        {
          name: "约会聚餐",
          keyword: "美食",
          kind: "part"
        },
        {
          name: "丽人SPA",
          keyword: "丽人",
          kind: "spa"
        },
        {
          name: "电影演出",
          keyword: "电影",
          kind: "movie"
        },
        {
          name: "品质出游",
          keyword: "旅游",
          kind: "travel"
        }
      ]
    }
  },
  computed:{
      cur(){
          return this.artistCategory[this.curIndex].child
      }
  },
  async mounted() {
    // this.handleOver(0,this.$store.state.geo.position.city)
    this.handleOver(0,'北京')
  },
  methods:{
      over(index){
        // let dom = e.target
        // let tag = dom.tagName.toLowerCase()
        // let city = this.$store.state.geo.position.city
        this.handleOver(index,"北京")

        // }
      },
      handleOver:async function(index,city){
            let category = this.artistCategory[index]
            // if (tag === 'dd') {
            let keyword = category.keyword
            // console.log(index)
            let {status,data:{count,pois}}=await this.$axios.get('/search/resultsByKeywords',{
                params:{
                    keyword,
                    // city:self.$store.state.geo.position.city
                    city:city
                }
            })
            if(status===200&&count>0){
                let r= pois.filter(item=>item.photos.length).map(item=>{
                    return {
                        title:item.name,
                        pos:item.type.split(';')[0],
                        price:item.biz_ext.cost||'暂无',
                        img:item.photos[0].url,
                        url:'//abc.com'
                    }
                })
                category.child = r.slice(0,9)
                // self.list[self.kind]=r.slice(0,9)
            }else{
                category.child = r.slice(0,9)
                // self.list[self.kind]=[]
            }
      }
  }
};
</script>

<style lang="scss" scoped>
@import "@/assets/css/index/artistic.scss";
</style>
