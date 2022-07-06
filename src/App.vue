<template>
  <div>
    <MyHeader title="我的购物车" backgroundColor='red' color="#000"></MyHeader>
    <div style="margin-top:45px">
      <MyGoods v-for="item in list" :key="item.id" :obj='item'></MyGoods>
    </div>
    <MyFooter></MyFooter>
  </div>
</template>

<script>
import MyHeader from './components/MyHeader'
import MyGoods from './components/MyGoods'
import MyFooter from './components/MyFooter'
export default {
  components: {
    MyHeader,
    MyGoods,
    MyFooter
  },
  data(){
    return{
      list:[],
    }
  },
  created () {
    this.$axios({
      url:'/api/cart',
    }).then((res)=>{
      console.log(res.data.list);
      this.list=res.data.list
    })
  }
}
</script>

<style>
</style>
