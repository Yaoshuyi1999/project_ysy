<template>
  <header class="header">
    <h1>todos</h1>
    <input id="toggle-all" class="toggle-all" type="checkbox" v-model="isAll">
    <label for="toggle-all"></label> 
    <!-- label 可以关联一个表单标签 -->
    <input
      class="new-todo"
      placeholder="输入任务名称-回车确认"
      autofocus
      v-model.trim="task"
      @keydown.enter="enter"
    />
    <!-- input绑定回车事件 -->
  </header>
</template>
// 输入任务敲击回车, 新增待办任务
<script>
export default {
  data () {
    return {
      task: ""
    }
  },
  methods: {
    enter(){
      //按下回车以后，增加一条数据
      // 这里是子组件要改变父组件list的数组值
      // 非空判断
      if(this.task.length==0){
        return alert('请输入任务')
      }
      this.$emit('add',this.task)
      this.task=''
    }
  },
  computed: {
    isAll:{
      get(){
        return this.$parent.list.every((ele)=>ele.isDone)
      },
      set(checked){
        this.$emit("setchecked",checked)
        // this.$parent.list.forEach((ele) => (ele.isDone =checked))
      }
    }
  }
}
</script>