<template>
  <ul class="todo-item" v-bind:class="{ 'is-complete':todo.completed }">
    <li>
      <span><input type="checkbox" @click="changeStatus" :checked="todo.completed == true"></span>
      <span>{{ todo.title }}</span>
      <button @click="$emit('delete-todo', todo.id)" >X</button>
    </li>
  </ul>
</template>

<script>

export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    changeStatus() {
      // eslint-disable-next-line vue/no-mutating-props
      this.todo.completed = !this.todo.completed
      console.log('some')
    }
  }
}
</script>

<style scoped>
  .is-complete{
    text-decoration: line-through;
  }
</style>