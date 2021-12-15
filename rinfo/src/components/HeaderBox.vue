<template>
  <div id="header">
    <img id="logo" alt="RINFO logo" src="@/assets/logo.png" />
    <div id="menu">
      <a> <img alt="Menu" src="@/assets/menu.png" /> </a>
    </div>
  </div>
</template>

<script>
export default {
  name: "HeaderBox",
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
div#menu {
  margin: auto 0;
}
div#menu a img {
  transition: all 0.3s ease-in;
}
div#menu a img:hover {
  transform: rotate(-90deg);
}
</style>
