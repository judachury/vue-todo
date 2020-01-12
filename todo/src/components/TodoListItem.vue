<template>
  <div>
    <div class="card">
      <div class="card-body">
        <h5 class="card-title">{{item.title}}</h5>
      </div>
      <h6 class="card-subtitle" :class="overdueCss" v-if="item.dueDate && !item.completed">
        <span v-show="item.dueDate.getTime() < Date.now()">{{dueDateLabel}}: {{formattedDate}}</span>
      </h6>
      <div class="todo-controls">
        <button class="btn sm btn-outline-success" @click.prevent="markCompleted">Completed</button>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: ["item"],
  computed: {
    formattedDate() {
      let dt = this.item.dueDate;
      return dt.getFullYear() + "-" + (dt.getMonth() + 1) + "-" + dt.getDate();
    },
    isOverdue() {
      return this.item.dueDate.getTime() < Date.now();
    },
    dueDateLabel() {
      return this.isOverdue ? "Overdue" : "Due";
    },
    overdueCss() {
      return {
        "text-danger": this.isOverdue,
        "text-uppercase": this.isOverdue
      };
    }
  },
  methods: {
    markCompleted() {
      this.item.completed = true;
      this.$emit("item-completed");
    }
  }
};
</script>

<style scoped>
.card {
  margin-top: 10px;
}
.card .todo-controls {
  position: absolute;
  top: 10px;
  right: 10px;
  visibility: hidden;
}
.card:hover .todo-controls {
  visibility: visible;
}
</style>