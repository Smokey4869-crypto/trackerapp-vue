<template>
  <form v-on:submit.prevent="onSubmit" class="add-form">
    <div class="form-control">
      <label>Task</label>
      <input type="text" v-model="text" name="text" placeholder="Add Task" />
    </div>
    <div class="form-control">
      <label>Day & Time</label>
      <input
        type="text"
        v-model="day"
        name="day"
        placeholder="Add Day & Time"
      />
    </div>
    <div class="form-control form-control-check">
      <label>Set Reminder</label>
      <input type="checkbox" v-model="reminder" name="reminder" />
    </div>

    <input type="submit" value="Save Task" class="btn btn-block" />
  </form>
</template>

<script lang="ts">
import { TaskModel } from "@/types/TaskModel";
import { Options, Vue } from "vue-class-component";

@Options({
    data() {
        return {
            text: '',
            day: '',
            reminder: false
        }
    }
})
export default class AddTask extends Vue {
    text!: string
    day!: string
    reminder!: boolean

    onSubmit() {
        if (!this.text) {
            alert('Please add a task')
            return
        }

        const newTask: TaskModel = {
            text: this.text,
            day: this.day,
            reminder: this.reminder
        }

        this.$emit('add-task', newTask)

        this.text = ''
        this.day = ''
        this.reminder = false
    }
}
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}
.form-control {
  margin: 20px 0;
}
.form-control label {
  display: block;
}
.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}
.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.form-control-check label {
  flex: 1;
}
.form-control-check input {
  flex: 2;
  height: 20px;
}
</style>