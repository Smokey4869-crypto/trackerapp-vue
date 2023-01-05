<template>
  <header>
    <h1>{{ title }}</h1>
    <Button 
      @btn-click="$emit('toggle-add-task')" 
      :text="showAddTask ? 'Close' : 'Add Task'" 
      :color="showAddTask ? 'red' : 'green'" />
  </header>
</template>

<script lang="ts">
import { Options, Vue } from "vue-class-component";
import Button from "./Button.vue";

@Options({
  props: {
    title: {
      type: String,
      default: "Hello World"
    },
    showAddTask: Boolean
  },
  components: {
    Button,
  }
})
export default class HeaderComponent extends Vue {
  title!: string
  showAddTask!: boolean
}
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>