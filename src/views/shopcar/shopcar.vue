<template>
  <div class="shopcar">
    shopcar
    <h1>实验路由</h1>
    <div v-for="(item,index) in shopItem" :key="index">
      <ComputedShops :item="item"></ComputedShops>
    </div>
  </div>
</template>

<script>
import {getCookie} from '@/until/cookie.js';
import {mapState} from 'vuex'
import ComputedShops from '@/components/computedShops/computedShops'
export default {
  data() {
    return {

    }
  },
  computed:{
    ...mapState(['shopItem'])
  },
  components:{ComputedShops},
  mounted(){
    console.log(this.shopItem)
    this.$http.post('/api/shoplist',{token:getCookie('keyword')}).then(res=>{
      if(res.code===0){
        this.$router.push({
          name:'login',
          query:{
            from:'shopcar'
          }
        })
      }else{
        console.log(res)
      }
    })
  }
}
</script>

<style scoped>
</style>
