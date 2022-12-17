<template>
  <div class="input-box expiration">
    <label for="persistent">
      <input id="persistent" type="radio" name="persistence" value="persist" v-model="type" @input="event => persist = event.target.value"/>
      Persistent
      <span class="tooltip" id="expiration-tooltip"></span>
    </label>

    <label for="time">
      <input id="time" type="radio" name="persistence" checked value="time" v-model="type" @input="event => persist = !event.target.value"/>
      Time
    </label>

    <label for="clicks">
      <input id="clicks" type="radio" name="persistence" value="clicks" v-model="type" @input="event => persist = !event.target.value"/>
      Clicks
    </label>

    <input type="number" name="expiration-timer" id="expiration-timer" v-model="timer" placeholder="Time (h) / Clicks" min="0" max="48" :disabled="persist"/>
  </div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "InputExpiration",
  data() {
    return {
      persist: false,
      type: '',
      timer: 0,
    }
  }
})
</script>

<style lang="scss">
.expiration {
  display: inline-flex;
  flex-direction: column;

  .tooltip {
    margin-left: 1.4rem;

    &::after {
      margin-left: -3rem;
      content: 'Determines how long the URL will continue linking to the destination. \A\A Persistent- The link will remain indefinitely, or until i fuck up the database \A Time- The URL will stop working after the amount of hours specified \A Clicks- The link will stop working after the amount of usages specified \A\A Note: If it is not set to persistent, the link will be automatically removed whenever the server restarts.';
    }
  }

  > * {
    margin: 0.2rem;
  }

  #expiration-timer {
    width: 9rem;
  }
}
</style>