<template>
  <v-app-bar
    elevate-on-scroll
    fixed
    app
    elevation="3"
    class="mt-md-4 mt-sm-4 mx-sm-6 mx-md-auto"
    style="
      background-color: white;
      max-width: 1024px !important;
      margin-left: auto;
      margin-right: auto;
      border-radius: 15px;
      -webkit-backdrop-filter: saturate(100%) blur(5px);
      backdrop-filter: saturate(100%) blur(10px);
    "
  >
    <v-app-bar-nav-icon
      class="d-md-none d-lg-none"
      @click="toggleDrawer"
    ></v-app-bar-nav-icon>

    <v-toolbar-title class="mr-4 px-0 google-font">
      <router-link
        to="/"
        class="text--secondary"
        style="text-decoration: none; font-size: 100%"
      >
        {{ devfestInfo.name }}
      </router-link>
    </v-toolbar-title>

    <div class="hidden-sm-and-down google-font">
      <template v-for="(page, index) in pages">
        <v-btn
          rounded
          text
          small
          :key="index"
          class="mr-1"
          color="primary"
          :to="page.path"
          v-if="page.visible == 1"
          style="text-transform: none; font-size: 80%; font-weight: 500"
          >{{ page.name }}</v-btn
        >
      </template>
      <v-btn
        rounded
        text
        small
        class="mr-1"
        color="primary"
        target="_blank"
        href="https://boson-higgs.link/"
        style="text-transform: none; font-size: 80%; font-weight: 500"
        >Boson Higgs</v-btn
      >
    </div>
  </v-app-bar>
</template>

<script>
import devfestJSON from "@/assets/data/devfests.json";
import navbarJSON from "@/assets/data/navbar.json";
export default {
  data: () => ({
    pages: navbarJSON,
    devfestInfo: devfestJSON,
  }),
  methods: {
    toggleDrawer() {
      this.$store.commit("TOGGLE_DRAWER");
    },
  },
};
</script>

<style></style>
