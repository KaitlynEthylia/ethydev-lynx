<template>
  <div class="theme-switcher-container" @click="toggleTheme">
    <span class="tickbox"></span>
    <img
      class="theme-switcher-icon"
      src="../../assets/svgs/light.svg"
      alt="Light theme icon"
      id="theme-light"
    />
    <img
      class="theme-switcher-icon"
      src="../../assets/svgs/night.svg"
      alt="Dark theme icon"
      id="theme-dark"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'ThemeSwitcher',
  methods: {
    toggleTheme() {
      this.$emit('toggleTheme')
    },
  },
})
</script>

<style lang="scss">
.theme-switcher-container {
  --outer-size: 2rem;
  --inner-size: 1.6rem;
  --margin-size: 0.2rem;
  --border-size: 1rem;

  display: inline-block;
  height: var(--outer-size);

  background-color: var(--colour-inset-dark);
  border-radius: var(--border-size);
  box-shadow: inset var(--shadow-low);
  cursor: pointer;
  margin: 1rem;

  .theme-switcher-icon {
    height: var(--inner-size);
    margin: var(--margin-size);

    filter: brightness(0.2);
    pointer-events: none;

    transition: var(--trans);
    &#theme-light {
      opacity: 0;
    }
  }

  .tickbox {
    content: '';
    height: var(--inner-size);
    width: var(--inner-size);
    margin: var(--margin-size);

    background-color: var(--colour-background-dark);
    border-radius: var(--border-size);

    position: absolute;
    transition: var(--trans);


    &:hover {
      scale: 1.1;
    }
  }
}

.dark {
  .theme-switcher-icon {
    filter: brightness(0.8);

    &#theme-light {
      opacity: 1;
    }

    &#theme-dark {
      opacity: 0;
    }
  }

  .tickbox {
    translate: var(--outer-size);
  }
}
</style>
