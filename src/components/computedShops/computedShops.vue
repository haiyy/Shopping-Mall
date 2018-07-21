<template>
    <div class="shopend">
       <div class="shopList">
            <dl>
                <dt><img v-lazy="item.show.img" alt=""></dt>
                <dd>
                    <div class="menu">
                        {{item.title}}
                    </div>
                    <div class="shops">
                        <div class="price">
                            <span>{{item.price}}</span>
                        </div>
                        <div class="increatment">
                            <span @click="last">-</span>
                            <b>{{1}}</b>
                            <span @click="next">+</span>
                        </div>
                    </div>
                </dd>
            </dl>
        </div>
    </div>
</template>

<script>
export default {
  props:{
    item:{
      type:Object,
      required:true
    }
  },
  data() {
    return {
      num:1,
      sum:''
    }
  },
  mounted(){
     this.last()
     this.next()
  },
  methods:{
      last(){
        this.num--;
        if(this.num<0){
           this.num=0;
        }
        this.$emit("total",{
            id:this.id,
            sum:this.price*this.num
        })
      },
      next(){
        this.num++;
        this.$emit("total",{
            id:this.id,
            sum:this.price*this.num
        })
      }
  }
}
</script>

<style scoped>
    .shopend{
        padding:0 10px;
    }
    .shopList dl{
        display:flex;
    }
    dl dt{
        width:1.5rem;
        height:1.5rem;
    }
    dl dt img{
        width:100%;
        height:100%;
    }
    dl dd{
        padding-left:10px;
        color:#666666;
    }
    dl dd .shops{
        display:flex;
        justify-content:space-between;
        padding:14px 0;
    }
     dl dd .price{
         color:#FC4141;
         font-size:18px;
         font-weight:800;
     }
     dl dd .increatment{
        border:1px solid #ccc;
        border-radius:6px;
        padding:0 10px;
     }
    dl dd .increatment span,dl dd .increatment b{
         width:15px;
        height:34px;
        line-height:34px;
         display:inline-block;
         text-align:center;
     }
     dl dd .increatment b{
         width:35px;
         text-align:center;
         border-left:1px solid #ccc;
         border-right:1px solid #ccc;
     }

</style>
