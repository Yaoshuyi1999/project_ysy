<template>
  <div class="box">
    <input type="search" placeholder="搜索-书本名称" class="search" @keydown.enter='enterFn' v-model.trim="enter">
    <button class="all" @click="getbook">全部</button>
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
      @bookDel='bookDel'
      @bookMore='bookMore'
      ></bookMan>
    </table>
    <bookAdd @bookAddFn='bookAddFn' ref="flag"></bookAdd>
  </div>
</template>

<script>
import bookMan from './components/bookMan'
import bookAdd from './components/bookAdd'
export default {
  components: {
    bookMan,
    bookAdd,
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
        // console.log(res);
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
        console.log(res);
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
      }).then(()=>{
          // this.list=res.data.data
          // console.log(res);
          this.getbook()
          alert('数据新增成功')
          this.$refs.flag.flag=false
      })
    },
    bookMore(id){
      let index=this.list.findIndex(ele=>ele.id==id)
      // console.log(this.list[index]);
      alert(`
      详情内容：

      书名:${this.list[index].bookname}
      作者:${this.list[index].author}
      出版商:${this.list[index].publisher}
      `)
      // console.log(id);
    },
    bookDel(id){
      // let index=this.list.findIndex(ele=>ele.id==id)
      // this.list.splice(index,1)
      this.$axios({
        url: '/api/delbook',
        params:{
          id:id,
        }
      }).then(()=>{
          this.getbook()
          alert('数据删除成功')
      })
    },
  }
}
</script>

<style scoped>
  .box{
    width: 900px;
  }
  .search{
    font-size: 15px;
    padding: 5px 0;
    padding-left: 10px;
    border: 1px solid #ccc;
  }
  .all{
    float: right;
    margin-right: 100px;
    margin-top: 5px;
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