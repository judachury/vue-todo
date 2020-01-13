<template>
  <div class="home">
    <TodoList :todos="todos" />
  </div>
</template>

<script>
import TodoList from "../components/TodoList.vue";
export default {
  name: "home",
  components: {
    TodoList
  },
  created() {
    this.todos = this.$todos.getItems();
  },
  data() {
    return {
      todos: []
      /* todos: [
        {
          title: "Setup environment",
          dueDate: new Date(2019, 0, 26),
          completed: false
        },
        {
          title: "Create main list component",
          dueDate: new Date(2020, 0, 26),
          completed: false
        },
        { title: "Display TODO items", completed: false }
      ] */
    };
  }
};
</script>
