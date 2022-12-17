<template>
  <form class="input" v-on:submit.prevent="post">
    <div class="top">
      <input type="url" name="destination" placeholder="Destination URL" v-model="url">
      <input type="submit" value="Upload" />
    </div>

    <div class="bottom">
      <InputExpiration ref="exp"></InputExpiration>
      <InputLink ref="link"></InputLink>
    </div>
  </form>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import InputExpiration from "./input/InputExpiration.vue";
import InputLink from "./input/InputLink.vue";

export default defineComponent({
  name: "Input",
  components: { InputLink, InputExpiration },
  data() {
    return {
      url: '',
    }
  },
  methods: {
    post() {
      const exp = <typeof InputExpiration> this.$refs.exp
      const link = <typeof InputLink> this.$refs.link
      const requestOptions = {
        method: "POST",
        headers: {
          "Content-Type": "application/json"
        },
        body: JSON.stringify({
          url: this.url,
          expiration: exp.type,
          timer: exp.timer,
          secret: link.secret,
          custom: link.custom,
          hashLength: link.hashLength,
          customURL: link.customURL,
        })
      }
      try {
        fetch("http://localhost:8085", requestOptions).then(response => {
          console.log(response)
        })
      } catch (e) {
        console.log(e)
      }
    },
  },
})
</script>

<style lang="scss">
.input-box {

  padding: 0.2rem;
  background-color: var(--colour-pink-light);
  border-radius: 1rem;
  box-shadow: var(--shadow-low);

  .tooltip{
    font-size: 1.2rem;
    color: var(--colour-pink-dark);

    &::after {
      white-space: pre-wrap;
      position: absolute;
      color: var(--text-colour);
      font-size: 0.5rem;
      word-wrap: break-word;
      width: 25rem;
      padding: 0.3rem;
      border-radius: 0.5rem;
      box-shadow: var(--shadow-low);
      margin-top: 1.25rem;
      background-color: var(--colour-inset-light);
      z-index: 2;

      opacity: 0;
      transition: opacity 0.2s;
      pointer-events: none;
    }
    &:hover::after {
      opacity: 1;
      transition-delay: 0.5s;
    }
  }
}

input {
  font-family: "CaskaydiaCove", "Roboto Light", sans-serif;


  &:not([type=submit]) { box-shadow: var(--shadow-low) inset; }

  border: none;
  border-radius: 0.6rem;
  padding: 0.2rem 0.5rem;

  &::-webkit-inner-spin-button, &::-webkit-outer-spin-button { -webkit-appearance: none; margin: 0; }
  &[type=number] {
    -moz-appearance: textfield;
  }
  &[type=url], &[type=text] {
    border-radius: 0.8rem;
  }

  &[type=url], &[type=text], &[type=number] {
    background-color: var(--colour-background-light);
    color: var(--text-colour);
    transition: filter 0.2s;

    &:disabled {
      filter: contrast(0.5);
    }
  }

  &[type=url] {
    width: 32rem;
    height: 1.8rem;
    font-size: 1.2rem;
  }

  &[type=submit] {
    border-radius: 0.8rem;
    height: 2.2rem;
    font-size: 1.2rem;
    margin-left: 1rem;
    box-shadow: var(--shadow-low);
    background-color: var(--colour-pink-light);
    width: 6rem;

    &:hover { filter: brightness(1.1); }
    &:active { filter: brightness(0.9); }
  }
}

.input {
  .top {
    width: 40rem;
  }

  .bottom > * {
    margin: 1rem;
  }

  display: flex;
  flex-direction: column;

  align-items: center;
  justify-content: center;
}

</style>
