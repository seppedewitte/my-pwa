<template>
  <div id="app">
    <h1>my cool PWA App</h1>
    <img alt="Vue logo" src="./assets/logo.png" />
    <button v-if="updateAvailable">click to update app</button>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  created() {
    document.addEventListener("swupdatefound", this.updateTheApp, {
      once: true,
    });
  },
  data: function () {
    return {
      registration: null,
      updateAvailable: false,
    };
  },
  methods: {
    updateTheApp(e) {
      this.registration = e.detail;
      this.updateAvailable = true;
    },
    update() {
      this.updateAvailable = false;
      if (this.registration || this.registration.waiting) {
        this.registration.waiting.postMessage({ type: "SKIP_WAITING" });
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
