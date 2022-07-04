<template>
  <div>
    <input type="search" placeholder="搜索-书本名称" class="search" @keydown.enter='enterFn' v-model.trim="enter">
    <table>
      <thead>
        <th>序号</th>
        <th>书名</th>
        <th>作者</th>
        <th>出版商</th>
        <th>操作</th>
      </thead>
      <bookMan 
      v-for="item in list" 
      :key="item.id" 
      :list="item"
      @bookMore='bookMore'
      ></bookMan>
    </table>
    <bookAdd @bookAddFn='bookAddFn' ref="flag"></bookAdd>
  </div>
</template>

<script>
import bookMan from './components/bookMan.vue'
import bookAdd from './components/bookAdd'
export default {
  components: {
    bookMan,
    bookAdd
  },
  data () {
    return {
      list:[],
      enter:'',
    }
  },
  created () {
    this.getbook()
  },
  methods: {
    getbook(){
      this.$axios({
        url: '/api/getbooks'
      }).then((res)=>{
        console.log(res);
          this.list=res.data.data
      })
    },
    enterFn(){
      if(this.enter.length==0){
        this.enter=''
      }
      // console.log(this.list.filter(ele=>ele.bookname==this.enter));
      this.$axios({
        url: '/api/getbooks',
        params:{
          bookname:this.enter
        }
      }).then((res)=>{
        // console.log(res.data.data);
        this.list=res.data.data
      })
      this.enter=''
    },
    bookAddFn(val){
      console.log(val);
      // this.list.push(val)
      this.$axios({
        url: '/api/addbook',
        method:'POST',
        data:val
      }).then((res)=>{
          // this.list=res.data.data
          console.log(res);
          this.getbook()
          alert('数据新增成功')
          this.$refs.flag.flag=false
      })
    },
    bookMore(id){
      console.log(id);
    }
  }
}
</script>

<style scoped>
  .search{
    font-size: 15px;
    padding: 5px 0;
    padding-left: 10px;
    border: 1px solid #ccc;
  }
  table{
    margin-top: 10px;
    width: 800px;
    border-collapse: collapse;
    text-align: left;
  }
  th{
    border: 1px solid #ccc;
    height: 30px;
    padding-left: 5px;
  }
  thead{
    border-bottom: 2px solid black;
  }
</style>