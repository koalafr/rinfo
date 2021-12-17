<template>
  <div id="header">
    <img id="logo" alt="rinfo logo" src="@/assets/logo.png" />
    <AppMenu id="menu" @clicked="updateSources" :providers="providers" />
  </div>
</template>

<script>
import AppMenu from "./AppMenu.vue";

export default {
  name: "HeaderBox",
  components: {
    AppMenu,
  },
  props: ["providers"],
  methods: {
    updateSources(data) {
      this.$emit("updateSource", data);
    },
  },
};
</script>

<style scoped>
#header {
  margin: 0 auto;
  max-width: 1020px;
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  color: var(--primary-color);
}
img#logo {
  max-width: 200px;
  height: auto;
}
#menu {
  margin: auto 0;
}
</style>
