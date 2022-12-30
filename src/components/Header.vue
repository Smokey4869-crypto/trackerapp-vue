<template>
  <header>
    <h1>{{ title }}</h1>
    <Button text="Add Task" color="green"/>
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
    }
  },
  components: {
    Button,
  }
})
export default class HeaderComponent extends Vue {
  title!: string
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