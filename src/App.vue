<template>
  <main class="main-page">
    <MainPage></MainPage>
  </main>
  <PageFooter></PageFooter>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import MainPage from "./components/MainPage.vue";
import PageFooter from "./components/PageFooter.vue";

export default defineComponent({
  name: "App",
  components: {PageFooter, MainPage}
})
</script>

<style lang="scss">
.main-page {
  height: 100vh;
}
</style>
