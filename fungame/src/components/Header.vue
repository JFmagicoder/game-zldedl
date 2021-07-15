<template>
  <div
    class="rounded-lg mt-12 pa-4 container"
    :style="{ borderColor: headerOutlineColor }"
  >
    <v-img :src="logo" max-height="100" max-width="100"></v-img>
    <div class="rounded-lg scoreCard pa-8">
      <span
        class="score_title font-weight-bold"
        :style="{ borderColor: scoreTextColor }"
        >SCORE</span
      >
      <span
        class="score_value font-weight-bold"
        :style="{ borderColor: darkTextColor }"
        >{{ winCounts }}</span
      >
    </div>
  </div>
</template>

<script>
import { headerOutline, scoreText, darkText } from "../constants/colors";
export default {
  props: ["winCounts"],
  data() {
    return {
      logo: require("../../../images/logo-bonus.svg"),
    };
  },
  computed: {
    headerOutlineColor() {
      return headerOutline;
    },
    scoreTextColor() {
      return scoreText;
    },
    darkTextColor() {
      return darkText;
    },
  },
};
</script>

<style scoped>
.container {
  border: solid;
  border-width: 2px;
  max-width: 600px;
  max-height: 200px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.scoreCard {
  background: white;
  width: 140px;
  height: 100px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
.score_title {
  font-size: 1rem;
  letter-spacing: 0.03125em;
}
.score_value {
  font-size: 3rem;
  line-height: 3.125rem;
}
</style>
