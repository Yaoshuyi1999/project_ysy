<template>
  <div>
    <MyTable :list="list">
      <template #thead>
        <th>#</th>
        <th>商品名称</th>
        <th>价格</th>
        <th>标签</th>
        <th>操作</th>
      </template>
      <template #tbody="scope">
        <td>{{scope.row.id}}</td>
        <td>{{scope.row.goods_name}}</td>
        <td>{{scope.row.goods_price}}</td>
        <td>
          <!-- {{scope.row.tags}} -->
          <input 
          type="text"
          class="tag-input form-control"
          style="width: 100px;"
          v-if="scope.row.inputVisible"
          v-focus
          @blur="scope.row.inputVisible=false"
          @keydown.enter="enterFn(scope.row)"
          v-model="scope.row.inputValue"
          @keydown.esc="scope.row.inputValue=''"
          >
          <button 
          v-else
          class="btn btn-primary btn-sm add-tag"
          style="display:block"
          @click="scope.row.inputVisible=true"
          >+Tag</button>
          <span v-for="(item,index) in scope.row.tags" :key="index" class="badge badge-warning" style="margin-right: 5px">
            {{item}}
          </span>
        </td>
        <td>
          <button class="btn btn-danger btn-sm" @click="del(scope.row.id)" v-show="flag">
            删除
          </button>
        </td>
      </template>
    </MyTable>
    <!-- 他只负责展示，而我获取的数据，下一次可能是不一样的。所以要在goolist里面进行请求 -->
  </div>
</template>

<script>
import axios from 'axios';
import MyTable from "../components/MyTable";
export default {
  components: {
    MyTable,
  },
  data () {
    return {
      list:[], 
      flag:false, 
      identitys:['admin','ysy','lhr'],
      identity:'ysy'
    }
  },
  created(){
    axios({
       url: "/api/goods",
    }).then((res) => {
      console.log(res);
      this.list = res.data.data;
    });
    if(this.identitys.indexOf(this.identity)==-1){
        this.flag=false
        return
      }else{
        this.flag=true
      }
  },
  methods: {
    del(id){
        const index=this.list.findIndex(ele=>ele.id===id)
        this.list.splice(index,1)
    },
    enterFn(obj){
      if(obj.inputValue.trim().length ===0){
        alert('请输入值：')
        return
      }
      obj.tags.push(obj.inputValue)
      obj.inputValue=''
    }
  }
}
</script>

<style lang="less" scoped>
.my-goods-list {
  .badge {
    margin-right: 5px;
  }
}
</style>