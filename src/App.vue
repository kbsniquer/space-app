<template>
  <div class="container">
    <img :src="nasaObject.url" />
    <h1>{{ nasaObject.title }}</h1>
    <p>{{ nasaObject.explanation }}</p>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      nasaObject: {},
    };
  },
  async created() {
    // GET request using fetch with async/await
    const res = await fetch(
      "https://api.nasa.gov/planetary/apod?api_key=NfcyTbFPzpRXHo1mBtpooTJ5WQ158AOK6aYzmwzq"
    );
    const data = await res.json();

    console.log(data);
    this.nasaObject = data;
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
