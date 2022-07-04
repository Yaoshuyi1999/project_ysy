<template>
  <div>
    <bookMan></bookMan>
  </div>
</template>

<script>
import bookMan from './components/bookMan.vue'
export default {
  components: {
    bookMan,
  },
  data () {
    return {
      bookObj:{
        id:'',
        bookname:'',
        author:'',
        publisher:'',
      }
    }
  },
  created () {
    this.$axios({
      url: '/api/getbooks'
    }).then((res)=>{
        console.log(res.data);
    })
  },
}
</script>

<style>

</style>