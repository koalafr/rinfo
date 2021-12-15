<template>
  <div class="infocard">
    <div class="information">
      <p class="date">{{ mdata.date }}</p>
      <h3>{{ mdata.title }}</h3>
      <p>{{ mdata.news }}</p>
      <p class="link">
        <a target="_blank" :href="mdata.link">Lire la suite ></a>
      </p>
    </div>
    <div class="photography">
      <a target="_blank" :href="mdata.link">
        <img :src="mdata.photoUrl" alt="photo" />
      </a>
    </div>
  </div>
</template>

<script>
export default {
  name: "InfoCard",
  props: {
    mdata: {},
  },
};
</script>

<style scoped>
.infocard {
  background: var(--background-shade-color);
  display: flex;
  margin: 0 auto;
  margin-top: 30px;
  padding: 15px;
  box-shadow: 3px 3px 6px var(--blackdrop-color);
  border-radius: 7px;
  min-height: 150px;
  max-width: 650px;
}
.information {
  background: url("../assets/bg.png") 0 0 no-repeat;
  display: flex;
  flex-direction: column;
  flex-basis: 60%;
}
.photography {
  text-align: right;
  vertical-align: middle;
  align-self: right;
  flex-basis: 40%;
  padding: 30px 5px;
}
.photography img {
  border-radius: 7px;
  right: 0px;
  max-width: 250px;
  height: auto;
}
h3,
p {
  margin: 2px 0;
  margin-right: 10px;
}
p.date {
  font-size: 80%;
}
a {
  text-decoration: none;
  color: var(--black-color);
}
a:hover {
  color: var(--blackdrop-color);
}
.information p.link {
  padding-top: 20px;
}

@media (max-width: 800px) {
  .infocard {
    flex-direction: column-reverse;
  }
  .photography {
    text-align: center;
  }
  .photography img {
    max-width: 350px;
    height: auto;
  }
}
</style>
