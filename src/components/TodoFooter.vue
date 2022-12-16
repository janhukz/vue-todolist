<template>
  <footer class="footer">
    <span class="todo-count">剩余<strong>数量值</strong>{{ count }}</span>
    <ul class="filters" @click="typeChange">
      <li>
        <a :class="{selected:isSelected ==='all'}" href="javascript:;" @click="isSelected = 'all'">全部</a>
      </li>
      <li>
        <a :class="{selected:isSelected === 'no'}" href="javascript:;" @click="isSelected = 'no'">未完成</a>
      </li>
      <li>
        <a :class="{selected:isSelected === 'yes'}" href="javascript:;" @click="isSelected = 'yes'">已完成</a>
      </li>
    </ul>
    <button class="clear-completed" @click="delAll" >清除已完成</button>
  </footer>
</template>

<script>
export default {
    data() {
        return {
            isSelected:"all"
        }
    },
    props:['arr'],

    computed: {
        count() {
            return this.arr.length
        }
    },

    methods:{
        delAll() {
            this.$emit("delAllList")
        },
        typeChange() {
            this.$emit("typeChange",this.isSelected)
        }
    }
}
</script>