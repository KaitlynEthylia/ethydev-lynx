<template>
  <footer>
    <span>There is currently nothing to put in the footer</span>
  </footer>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "PageFooter",
})
</script>

<style lang="scss">
footer {
  background-color: #666;
  color: var(--text-colour-inverted);
  display: flex;
  justify-content: center;
  align-items: center;
  height: 20vh;
  font-size: 0.5rem;
  border-top: solid 0.1rem var(--text-colour);
}
</style>
