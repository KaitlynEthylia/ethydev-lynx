<template>
  <Logo></Logo>
  <Input></Input>
  <header class="page-header">
    <ThemeSwitcher @toggleTheme="toggleTheme"></ThemeSwitcher>
    <div class="separator">
      <ListButton></ListButton>
    </div>
  </header>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Logo from "./mainpage/Logo.vue";
import ThemeSwitcher from "./mainpage/ThemeSwitcher.vue";
import Input from "./mainpage/Input.vue";
import ListButton from "./mainpage/ListButton.vue";

export default defineComponent({
  name: "MainPage",
  components: { ListButton, Logo, ThemeSwitcher, Input },
  methods: {
    toggleTheme() {
      document.body.classList.toggle("dark")
    },
  },
})
</script>

<style lang="scss">
.page-header {
  display: flex;
  align-items: center;
  position: fixed;
  top: 0;
}
</style>
