<template>
  <button @click="onClick()" :style="{ background: color }" class="btn">
    {{ text }}
  </button>
</template>



<script lang="ts">
import { Options, Vue } from "vue-class-component";

@Options({
  props: {
    text: String,
    color: String,
  },
})
export default class Button extends Vue {
  text!: string;
  color!: string;

  onClick() {
    this.$emit("btn-click");
  }
}
</script>