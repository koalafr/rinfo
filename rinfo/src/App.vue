<template>
  <HeaderBox />
  <HelloWorld msg="Welcome" />

  <div v-for="item of items" :key="item.title">
    <InfoCard :mdata="item" />
  </div>
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
  data() {
    return {
      rssUrl: "https://www.francetvinfo.fr/titres.rss",
      items: [],
    };
  },
  methods: {
    async getRss() {
      const res = await fetch(
        `https://api.allorigins.win/get?url=${this.rssUrl}`
      );
      const { contents } = await res.json();
      const feed = new window.DOMParser().parseFromString(contents, "text/xml");
      const items = feed.querySelectorAll("item");
      this.items = [...items].map((el) => ({
        title: el.querySelector("title").innerHTML,
        news: this.cleanNews(el.querySelector("description").innerHTML),
        date: el.querySelector("pubDate").innerHTML,
        link: el.querySelector("link").innerHTML,
        photoUrl: el.querySelector("enclosure").getAttribute("url"),
      }));
    },
    cleanNews(dirty) {
      let clean = dirty
        .replace("<![CDATA[", "")
        .replace("]]>", "")
        .replace("&nbsp;", " ")
        .replace(".&nbsp;", " ");
      return clean;
    },
  },
  created: function () {
    this.getRss();
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
h3 {
  font-size: 18px;
}
</style>
