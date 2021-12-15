<template>
  <HeaderBox />
  <HelloWorld msg="Welcome" />
  <InfoCard headline="Big HeadLine on Stuff" />
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import HeaderBox from "./components/HeaderBox.vue";
import InfoCard from "./components/InfoCard.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
    HeaderBox,
    InfoCard,
  },
};
</script>

<style>
:root {
  --primary-color: #4fb2b2;
  --primary-shade-color: #20605d;
  --background-color: #f9f6de;
  --background-shade-color: #f2efe2;
  --black-color: #2c3e50;
  --blackdrop-color: #2c3e5033;
}
html {
  background-color: var(--background-color);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: var(--primary-shade-color);
  margin-top: 10px;
}
</style>
