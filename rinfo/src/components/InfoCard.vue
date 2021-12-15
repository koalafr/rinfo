<template>
  <div class="infocard">
    <h3>{{ headline }}</h3>
    <p>Info Goes Here</p>
  </div>
</template>

<script>
export default {
  name: "InfoCard",
  props: {
    headline: String,
  },
};
</script>

<style scoped>
.infocard {
  margin: 0 auto;
  margin-top: 30px;
  padding: 15px;
  box-shadow: 3px 3px 6px var(--blackdrop-color);
  border-radius: 7px;
  min-height: 150px;
  max-width: 600px;
  background-color: var(--background-shade-color);
}
</style>
