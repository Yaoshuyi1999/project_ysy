<template>
  <ul class="todo-list">
    <!-- completed: 完成的类名 -->
    <!-- 循环， -->
    <li :class="{completed:item.isDone}" v-for="item in list" :key="item.id">
      <div class="view">
        <!-- 判断前面是否是打钩状态 -->
        <input class="toggle" type="checkbox" v-model="item.isDone"/>
        <!-- 放入循环的值 -->
        <label>{{item.name}}</label>
        <button class="destroy" @click="del(item.id)"></button>
      </div>
    </li>
  </ul>
</template>

<script>
export default {
  //1.2
  props: {
    list:{
      type:Array,
      default:()=>[],
    }
  },
  methods: {
    del(id){
      this.$emit("del",id)
    }
  }
}
</script>