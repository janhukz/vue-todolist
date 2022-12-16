<template>
      <section class="todoapp">
    <!-- 除了驼峰, 还可以使用-转换链接 -->
    <TodoHeader :arr="list" @addList="add"></TodoHeader>
    <TodoMain :arr="showArr" @delList="del"></TodoMain>
    <TodoFooter :arr="list" @delAllList="delAll" @typeChange="filter"></TodoFooter>
  </section>
</template>

<script>
import './styles/base.css'
import './styles/index.css'
import TodoHeader from './components/TodoHeader.vue'
import TodoMain from './components/TodoMain.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  components:{
    TodoHeader,
    TodoMain,
    TodoFooter,
  },
  data() {
    return {
      list: JSON.parse(localStorage.getItem("TodoList")) || [],
      type:'all'
    };
  },
  methods:{
    add(name) {
      let id = this.list.length === 0 ? 100 :this.list[this.list.length-1].id + 1
      this.list.push({
        id:id,
        name:name,
        isDone:false
      })
    },
    del(id) {
      // 根据传过来的id取索引值
      // console.log(id)
      const isEqual = (obj) => obj.id === id
      const index = this.list.findIndex(isEqual)
      // console.log(index)
      this.list.splice(index,1)
    },
    delAll() {
      this.list = this.list.filter(obj=>obj.isDone === false)
    },
    filter(type) {
      this.type = type
    }
  },
  computed:{
    showArr() {
      if(this.type === 'yes') {
        return this.list.filter(obj=>obj.isDone === true)
      }else if (this.type === 'no') {
        return this.list.filter(obj=>obj.isDone === false)
      }else {
        return this.list
      }
    }
  },
  watch:{
    list: {
      handler() {
        localStorage.setItem('TodoList',JSON.stringify(this.list))
      },
      deep:true
    }
  }
}
</script>

<style>

</style>