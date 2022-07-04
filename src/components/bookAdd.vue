<template>
  <div>
    <input type="text" placeholder="书名" class="text" v-model.trim="obj.bookname">
    <input type="text" placeholder="作者" class="text" v-model.trim="obj.author">
    <input type="text" placeholder="出版社" class="text" v-model.trim="obj.publisher">
    <button @click="bookAddFn" :disabled="flag" :class="{bgc:flag}">新增</button>
  </div>
</template>

<script>
export default {
    data () {
        return {
            obj:{
                // id:'',
                bookname:'',
                author:'',
                publisher:''
            },
            flag:false
        }
    },
    methods: {
        bookAddFn(){
            this.flag=true
            if(this.obj.bookname==''||this.obj.author==''||this.obj.publisher==''){
                alert('请添加完整信息')
            }else{
                this.$emit('bookAddFn',this.obj)
                console.log(this.obj);
            }
            this.obj.bookname='';
            this.obj.author='';
            this.obj.publisher=''
        }
    }
}
</script>

<style scoped>
  .text{
    font-size: 15px;
    padding: 5px 0;
    padding-left: 10px;
    display: block;
    margin-top: 10px;
    width: 300px;
    border: 1px solid #ccc;
  }
  button{
    margin-top: 10px;
    background-color: rgb(54, 99, 223);
    color: white;
    padding: 5px 8px;
    border: none;
    border-radius: 3px;
  }
  .bgc{
    background-color: #999;
  }
</style>