<template>
    <dl @click="shopItem">
      <dt>
        <img v-lazy="item.show.img" alt="">
      </dt>
      <dd>
        <p class="tits">{{item.title}}</p>
        <p @click.stop="shopCar">
          <span>{{item.price}}</span>
          <i class="iconfont icon-shopcar"></i>
        </p>
      </dd>
    </dl>
</template>

<script>
import {getCookie} from '@/until/cookie.js'
export default {
  props:['item'],
  data() {
    return {

    }
  },
  methods: {
    shopCar(){
      this.$http.post('/api/shopcar',{
        token:getCookie('keyword'),
        item:this.item
      }).then(res=>{
        if(res.code===1){
          this.$store.commit('shopItems',res.msg)
        }else{
          console.log('写入失败')
        }
      })
    },
    shopItem(){
      this.$router.push({
        name:'detail',
        query:{
          imgUrl:this.item.show.img,
          price:this.item.price
        }
      })
    }
  }
}
</script>

<style lang="scss" scoped>
  dl{
    width:100%;
    color:#666;
    padding: 3px;
    dt{
      width:100%;
      img{
        width:100%;
        height: 5rem;
      }
    }
    dd{
      .tits{
        display:-webkit-box;
        -webkit-box-orient:vertical;
        -webkit-line-clamp:2;
        word-break:break-all;
        overflow:hidden;
        text-overflow:ellipsis;
      }
      p{
        display: flex;
        line-height: 2;
        justify-content: space-between;
        span{
          color:#ff3333;
        }
        i{
          text-align:center;
          width:30px;

        }
      }
    }
  }
</style>
