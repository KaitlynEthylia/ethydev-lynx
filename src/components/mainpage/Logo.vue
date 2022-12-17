<template>
  <div class="logo">
    <img src="../../../resources/favicon.svg" alt="Lynx Logo">
    <span>Lynx</span>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "Logo",
})
</script>

<style lang="scss">
.logo {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 5rem;

  img {
    height: 8rem;
    margin-right: 2rem;
  }

  span {
    font-size: 8rem;
    color: var(--text-colour);
  }
}
</style>
