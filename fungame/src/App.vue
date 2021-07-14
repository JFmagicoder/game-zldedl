<template>
  <v-app :style="{ background: createBackgroundString }">
    <v-main>
      <Home />
    </v-main>
  </v-app>
</template>

<script>
import Home from "./components/Home";
import {
  backgroundGradientStart,
  backgroundGradientEnd,
} from "./constants/colors";

export default {
  name: "App",

  components: {
    Home,
  },

  data() {
    return {};
  },

  computed: {
    createBackgroundString() {
      return `linear-gradient(to bottom, ${backgroundGradientStart}, ${backgroundGradientEnd})`;
    },
  },
};
</script>

<style>
@font-face {
  font-family: "BarlowSemiCondensed";
  src: local("BarlowSemiCondensed"),
    url(./fonts/BarlowSemiCondensed-Medium.ttf) format("truetype");
}
.v-application {
  font-family: "BarlowSemiCondensed" !important;
}
</style>
