<template>
  <AddTask v-show="showAddTask" @add-task="addTask" />
  <Tasks
    @toggle-reminder="toggleReminder"
    @delete-task="deleteTask"
    :tasks="tasks"
  />
</template>

<script lang="ts">
import { Options, Vue } from "vue-class-component";
import Tasks from "../components/Tasks.vue";
import AddTask from "../components/AddTask.vue";
import { TaskModel } from "../types/TaskModel";

@Options({
  components: {
    Tasks,
    AddTask,
  },
  data() {
    return {
      tasks: [] as TaskModel[],
    };
  },
  props: {
    showAddTask: Boolean,
  },
  async created() {
    this.tasks = await this.fetchTasks();
  },
})
export default class Home extends Vue {
  tasks!: TaskModel[];
  showAddTask!: boolean;

  //methods
  async addTask(task: TaskModel) {
    const res = await fetch("api/tasks", {
      method: "POST",
      headers: {
        "Content-type": "application/json",
      },
      body: JSON.stringify(task),
    });

    const data = await res.json();

    this.tasks = [...this.tasks, data];
  }

  async deleteTask(id: string) {
    if (confirm("Are you sure?")) {
      const res = await fetch(`api/tasks/${id}`, {
        method: "DELETE",
      });

      res.status === 200
        ? (this.tasks = this.tasks.filter((task) => task.id !== id))
        : alert("Something went wrong");
    }
  }

  async toggleReminder(id: string) {
    const taskToToggle: TaskModel = await this.fetchTask(id);
    const updateTask = { ...taskToToggle, reminder: !taskToToggle.reminder };

    const res = await fetch(`api/tasks/${id}`, {
      method: "PUT",
      headers: {
        "Content-type": "application/json",
      },
      body: JSON.stringify(updateTask),
    });

    const data = await res.json();

    this.tasks = this.tasks.map((task) =>
      task.id === id ? { ...task, reminder: data.reminder } : task
    );
  }
  async fetchTasks() {
    const res = await fetch("api/tasks");
    const data = await res.json();

    return data;
  }

  async fetchTask(id: string) {
    const res = await fetch(`api/tasks/${id}`);
    const data = await res.json();

    return data;
  }
}
</script>