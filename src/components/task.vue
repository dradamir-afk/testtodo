<template>
  <p v-bind:class="{'donetask': isDone}">
    <input type="checkbox" v-model="isDone" />
    <label class="taskName">{{task.name}}</label>
    <button class="btnRemove" @click="remove">Remove</button>
  </p>
</template>

<script>
export default {
  name: "task",
  props: ["task", "taskIndex"],
  data() {
    return {};
  },
  computed: {
    isDone: {
      get() {
        return this.task ? this.task.status : false;
      },
      set(status) {
        this.$emit("changeStatus", { status: status, index: this.taskIndex });
      }
    }
  },
  methods: {
    remove() {
      this.$emit("removeTask", this.taskIndex);
    }
  }
};
</script>

<style scoped>
.donetask {
  text-decoration: line-through;
  color: rgb(0, 0, 0);
}
.btnRemove{
  margin-left: 10px;
}
.taskName{
  margin-left: 10px;
}
</style> 