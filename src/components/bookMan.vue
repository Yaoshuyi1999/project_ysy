<template>
   <tbody>
        <tr>
          <td>{{list.id}}</td>
          <td>{{list.bookname}}</td>
          <td>{{list.author}}</td>
          <td>{{list.publisher}}</td>
          <td><button>删除</button><button @click="bookMore(list.id)">详情</button></td>
        </tr>
      </tbody>
</template>

<script>

export default {
  props: {
    list:{
      type: Object,
      default:()=>({})
    }
  },
  methods: {
    bookMore(id){
      alert(id)
      this.$emit('bookMore',id)
    }
  }

}
</script>

<style scoped>
  td{
    border: 1px solid #ccc;
    height: 30px;
    padding-left: 5px;
  }
</style>