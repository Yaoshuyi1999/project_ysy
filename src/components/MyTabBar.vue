<template>
  <div class="my-tab-bar">
  	<div 
        class="tab-item" 
        v-for="(item,index) in list" 
        :key="index"
        :class="{current:currentIndex==index}"
        @click="btn(item,index)"
    >
      <!-- 图标 -->
      <span class="iconfont" :class="item.iconText"></span>
      <!-- 文字 -->
      <span>{{item.text}}</span>
    </div>
  </div>
</template>

<script>
export default {
    data () {
        return {
            currentIndex:0,      
        }
    },
    props: {
        list:{
            type:Array,
            default:()=>[],
            required:true,
            validator(value){
                if(value.length>=2&&value.length<=5){
                    return true;
                }else{
                    return false;
                }
            },
        }
    },
    methods: {
        btn(item,index){
            this.currentIndex=index;
            this.$emit('btnFn',item.componentName)
        }
    }
}
</script>

<style lang="less" scoped>
.my-tab-bar {
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  height: 50px;
  border-top: 1px solid #ccc;
  display: flex;
  justify-content: space-around;
  align-items: center;
  background-color: white;
  .tab-item {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
}
    
.current {
  color: #1d7bff;
}
</style>