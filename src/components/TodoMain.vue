<template>
  <ul class="todo-list">
    <!-- completed: 完成的类名 -->
    <li :class="{ completed: obj.isDone }" v-for="obj in arr" :key="obj.id">
      <div class="view">
        <input class="toggle" type="checkbox" v-model="obj.isDone" />
        <label>{{ obj.name }}</label>
        <button class="destroy" @click="delOne(obj.id)"></button>
      </div>
    </li>
  </ul>
</template>

<script>
export default {
  props: ['arr'],

  methods: {
    delOne(id) {
      this.$emit("delList",id)
    }
  }
}
</script>
