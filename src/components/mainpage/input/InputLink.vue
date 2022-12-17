<template>
  <div class="input-box link">
    <label for="secret">
      <input type="checkbox" name="secret" id="secret" />
      Secret
    </label>

    <label for="hash">
      <input type="radio" checked name="hash-type" id="hash" @input="event => custom = !event.target.checked" />
      Hash
      <span class="tooltip" id="link-tooltip"></span>
    </label>


    <label for="custom">
    <input type="radio" name="hash-type" id="custom" @input="event => custom = event.target.checked" />
      Custom URL</label>

    <input id="hash-length" type="number" name="hash-length" v-model="hashLength" min="3" max="64" placeholder="Hash Length" :disabled="custom">
    <input id="custom-url" type="text" name="custom-url" v-model="customURL" placeholder="https://lynx.ethy.dev/..." pattern="[-a-zA-Z0-9_+=]+" :disabled="!custom">
  </div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "InputLink",
  data() {
    return {
      custom: true,
      hashLength: 6,
      secret: false,
      customURL: '',
    }
  },
})
</script>

<style lang="scss">
.link {
  display: inline-grid;

  .tooltip {
    margin-left: 2.1rem;

    &::after {
      content: 'Secret- If this is set, the link will not appear in the public list of links \A\A Hash- If this is set the link will simply be generated as a hash of characters, the default length is 6 but others can be specified \A Custom URL- Allows you to set how you want a link to appear, for example you could set https://lynx.ethy.dev/not-a-rockroll to link to \'Never Gonna Give You Up\'';
      margin-left: -16rem;
    }
  }

  #custom-url {
    grid-column-start: 1;
    grid-column-end: 3;
  }

  > * {
    margin: 0.2rem;
  }

  #hash-length {
    width: 6rem;
  }
}
</style>