<template>
  <button class="link-button" @click="toggleList(); this.$refs.linklist.getLinks(showList)">
    <span class="link-button-text">View Links</span>
  </button>
  <LinkList v-show="showList" ref="linklist" @closeList="closeList"></LinkList>
</template>

<script>
import { defineComponent } from "vue";
import LinkList from "./LinkList.vue";

export default defineComponent({
  name: "ListButton",
  components: {LinkList},
  data() {
    return {
      showList: false
    }
  },
  methods: {
    toggleList() { this.showList = !this.showList },
    closeList() { this.showList = false },
  }
})
</script>

<style lang="scss">
.link-button {
  height: 2rem;
  border: none;
  border-radius: 1rem;
  box-shadow: var(--shadow-low);
  background-color: var(--colour-pink-light);

  .link-button-text {
    font-size: 0.8rem;
    font-family: CaskaydiaCove, "Roboto Light", sans-serif;
    margin: 0 0.5rem
  }

  &:hover { filter: brightness(1.1); }
  &:active { filter: brightness(0.9); }
}
</style>
