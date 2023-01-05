<template>
  <div>
    <div v-for="task in tasks" v-bind:key="task.id">
      <Task @toggle-reminder="$emit('toggle-reminder', task.id)" @delete-task="$emit('delete-task', task.id)" :task="task" />
    </div>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from "vue-class-component";
import { TaskModel } from "../types/TaskModel";
import Task from "./Task.vue";

@Options({
  components: {
    Task,
  },
  props: {
    tasks: Array,
  },
//   emits: ['delete-task']
})
export default class Tasks extends Vue {
  tasks!: [TaskModel];
}
</script>