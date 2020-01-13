<template>
  <div class="list-container">
    <ul class="nav nav-tabs">
      <li class="nav-item">
        <a
          href="#"
          class="nav-link"
          :class="{active: filterType === false}"
          data-toggle="tab"
          @click.prevent="filterType = false"
        >Incompleted</a>
      </li>
      <li class="nav-item">
        <a
          href="#"
          class="nav-link"
          :class="{active: filterType === true}"
          data-toggle="tab"
          @click.prevent="filterType = true"
        >Completed</a>
      </li>
      <li class="nav-item">
        <a
          href="#"
          class="nav-link"
          :class="{active: filterType === undefined}"
          data-toggle="tab"
          @click.prevent="filterType = undefined"
        >All</a>
      </li>
    </ul>
    <TodoListItem
      v-for="(item, index) in filteredItems"
      :key="index"
      :item="item"
      @item-completed="filter"
    />
  </div>
</template>
<script>
import TodoListItem from "./TodoListItem.vue";
export default {
  props: ["todos"],
  components: { TodoListItem },
  data() {
    return {
      filteredItems: this.todos.filter(item => !item.completed),
      filterType: false
    };
  },
  watch: {
    filterType() {
      this.filter();
    }
  },
  methods: {
    filter() {
      console.log(this);
      if (this.filterType === true) {
        this.filteredItems = this.todos.filter(item => item.completed);
      } else if (this.filterType === false) {
        this.filteredItems = this.todos.filter(item => !item.completed);
      } else {
        this.filteredItems = this.todos;
      }
    }
  }
};
</script>
<style scoped>
.list-container {
  margin-top: 15px;
}
</style>