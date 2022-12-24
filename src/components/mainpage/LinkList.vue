<template>
  <div class="list-container" @click="this.$emit('closeList')">
    <div class="list-wrapper">
      <table class="list" @click.stop>
        <tr>
          <th>Link</th>
          <th>Destination</th>
          <th>Expiration</th>
          <th>Timer</th>
        </tr>
        <tr v-for="link in links">
          <td>{{ link.link }}</td>
          <td>{{ link.destination }}</td>
          <td>{{ link.expiration }}</td>
          <td>{{ link.timer }}</td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "LinkList",
  data() {
    return {
      links: [],
    }
  },
  methods: {
    getLinks(show) {
      if(!show) { return }
      this.links = []
      fetch(import.meta.env.VITE_SHORTY_URL, {
        method: "GET",

      }).then(response => {
        response.json().then(json => {
          for(const object in json) {
            const link = json[object]

            let expiration
            if(link.persist) { expiration = "Persist" }
            else if(link.expirationTime !== 9223372036854776000) { expiration = "Time" }
            else { expiration = "Clicks" }

            let timer
            switch (expiration) {
              case "Time": timer = link.expirationTime; break
              case "Clicks": timer = link.clickLimit; break;
            }

            this.links.push({
              link: object,
              destination: link.url,
              expiration: expiration,
              timer: timer,
            })
          }
        })
      })
    }
  }
})
</script>

<style lang="scss">

.list-container {
  background-color: #0006;
  position: fixed;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;

  .list-wrapper {
    position: relative;
    background-color: var(--colour-background-light);
    width: 80vw;
    height: 80vh;
    top: 10vh;
    left: 10vw;
    box-shadow: var(--shadow-low);
    transition: var(--trans);
    border-radius: 3rem;
    color: var(--text-colour);
    overflow: scroll;

    .list {
      position: relative;
      border-spacing: 0.4rem;
      overflow: hidden;
      width: 80vw;

      th, td {
        text-align: center;
        height: 1.8rem;
        border-bottom: solid #fd99ff20 1px;
      }

      th {
        font-size: 1.1rem;
      }

      th + th {
        border-left: solid var(--colour-pink-dark) 1px;
      }

      td + td {
        border-left: solid var(--colour-pink-light) 1px;
      }
    }
  }
}
</style>
