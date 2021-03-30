<template>
  <div v-bind:key="pic" v-for="pic in nasaPicArray">
    <img :src="pic" alt="" class="bkg" />
  </div>
  <Button />
</template>

<script>
import Button from "./components/Button";

export default {
  name: "App",
  components: {
    Button,
  },
  data() {
    return {
      nasaObject: {},
      nasaPicArray: [],
      nasaIds: ["PIA12348", "PIA15985", "0302063", "PIA15416", "PIA16008"],
    };
  },
  async created() {
    // GET request using fetch with async/await
    const data = await Promise.all(
      this.nasaIds.map(async (id) => {
        const res = await fetch(`https://images-api.nasa.gov/asset/${id}`);
        const data = await res.json();
        return data;
      })
    );
    this.nasaPicArray = this.moveIds(data);
  },
  methods: {
    moveIds(data) {
      return data.map((el) => el.collection.items[0].href);
    },
  },
};
</script>

<style>
body,
html,
p {
  margin: 0;
}
div {
  display: inline-block;
  overflow: hidden;
  position: relative;
  width: 100%;
}
.bkg {
  /* pointer-events: none;
  /* position: absolute; */
  width: 100%;
  /* height: 100%; */
  /* z-index: -1; */
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
