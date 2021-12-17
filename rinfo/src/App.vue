<template>
  <HeaderBox @updateSource="reloadFeed" />
  <HelloWorld msg="Welcome" :newsSources="newsSources"/>

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
      newsSources: ["Franceinfo"],
    };
  },
  methods: {
    reloadFeed(updatedSources) {
      if (JSON.stringify(this.newsSources) != JSON.stringify(updatedSources)) {
        this.newsSources = updatedSources;
        this.items = [];
        updatedSources.forEach((element) => {
          if (element === "Franceinfo") {
            this.getRss();
            console.log("refresh");
          }
        });
      }
    },
    async getRss() {
      const res = await fetch(
        `https://api.allorigins.win/get?url=${this.rssUrl}`
      );
      const { contents } = await res.json();
      const feed = new window.DOMParser().parseFromString(contents, "text/xml");
      const items = feed.querySelectorAll("item");
      this.items = [...items].map((el) => ({
        title: this.safegetXML(el, "title"),
        news: this.cleanNews(this.safegetXML(el, "description")),
        date: this.safegetXML(el, "pubDate"),
        link: this.safegetXML(el, "link"),
        photoUrl:
          (el.querySelector("enclosure") &&
            el.querySelector("enclosure").getAttribute("url")) ||
          "",
        source: "franceinfo",
      }));
    },
    safegetXML(el, selectMe) {
      if (!el) return "";
      let selected = el.querySelector(selectMe);
      if (!selected) {
        return "";
      }
      return selected.innerHTML;
    },
    cleanNews(dirty) {
      let clean = dirty
        .replace("<![CDATA[", "")
        .replace("]]>", "")
        .replace("&quot;", "'")
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
