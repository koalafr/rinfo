<template>
  <div>
    <a href="#" id="show-modal" @click="menuClicked">
      <img :class="{ active: showModal }" alt="Menu" src="@/assets/menu.png" />
    </a>
    <div id="menu-modal" v-if="showModal">
      <div class="menu-choice">
        <input
          type="checkbox"
          id="Franceinfo"
          value="Franceinfo"
          v-model="checkedSources"
        />
        <label for="Franceinfo">Franceinfo</label>
      </div>
      <div class="menu-choice">
        <input
          type="checkbox"
          id="LeMonde"
          value="LeMonde"
          v-model="checkedSources"
        />
        <label for="LeMonde">Le Monde</label>
      </div>
      <div class="menu-choice">
        <input
          type="checkbox"
          id="LeFigaro"
          value="LeFigaro"
          v-model="checkedSources"
        />
        <label for="LeFigaro">Le Figaro</label>
      </div>
      <br />
      <span>Sources: {{ checkedSources }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "AppMenu",
  data() {
    return {
      showModal: false,
      checkedSources: ["Franceinfo"],
    };
  },
  methods: {
    menuClicked() {
      this.showModal = !this.showModal;
      if (!this.showModal) {
        this.$emit("clicked", this.checkedSources);
      }
    },
  },
};
</script>

<style scoped>
a img {
  transition: all 0.3s ease-in;
}
.active {
  transform: rotate(-90deg);
  opacity: 0.5;
}
a img:hover {
  transform: rotate(-90deg);
}

#menu-modal {
  position: absolute;
  background: var(--primary-color);
  color: var(--background-color);
  transform: translate(-250px, 20px);
  width: 250px;
  border-radius: 7px;
  border-top-right-radius: 0;
  padding: 15px;
}

.menu-choice {
  font-size: 1.2em;
  padding: 5px;
}

.menu-choice input {
  margin-right: 10px;
}
</style>
