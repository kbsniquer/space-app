<template>
  <div class="container">
    <!-- <img :src="nasaObject.collection.items[0].href" /> -->
    <!-- <h1>{{ nasaObject.title }}</h1>
    <p>{{ nasaObject.explanation }}</p> -->
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
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
    this.nasaPicArray = JSON.stringify(this.moveIds(data));
  },
  methods: {
    moveIds(data) {
      return data.map((el) => el.collection.items[0].href);
    },
  },
};
</script>

<style>
img {
  width: 80%;
}

p {
  margin: 0 auto;
  width: 75%;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.container {
  max-width: 80%;
  margin: 0 auto;
  overflow: auto;
  border-radius: 5px;
}
</style>
