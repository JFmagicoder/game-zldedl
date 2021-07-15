<template>
  <div class="home-container">
    <Header :points="points" />
    <div class="content" v-if="!userSelected">
      <img :src="pentagon" />
    </div>
    <div style="height: 0px" v-if="!userSelected">
      <v-btn
        height="120"
        :style="scissorsStyle"
        class="circle_button"
        @click="userPick('scissors')"
      >
        <div class="circle_button_inner">
          <img :src="scissors" />
        </div>
      </v-btn>
      <v-btn
        height="120"
        :style="paperStyle"
        class="circle_button"
        @click="userPick('paper')"
      >
        <div class="circle_button_inner">
          <img :src="paper" />
        </div>
      </v-btn>
      <v-btn
        height="120"
        :style="rockStyle"
        class="circle_button"
        @click="userPick('rock')"
      >
        <div class="circle_button_inner">
          <img :src="rock" />
        </div>
      </v-btn>
      <v-btn
        height="120"
        :style="lizardStyle"
        class="circle_button"
        @click="userPick('lizard')"
      >
        <div class="circle_button_inner">
          <img :src="lizard" />
        </div>
      </v-btn>
      <v-btn
        height="120"
        :style="cyanStyle"
        class="circle_button"
        @click="userPick('cyan')"
      >
        <div class="circle_button_inner">
          <img :src="cyan" />
        </div>
      </v-btn>
    </div>
    <div class="play_mode_container" v-if="userSelected">
      <div>
        <p class="pick_title font-weight-bold text-center">YOU PICKED</p>
        <v-btn
          height="180"
          :style="gradientStyle(userSelectedName)"
          class="circle_button_large"
          disabled
        >
          <div class="circle_button_inner_large">
            <img :src="optionImage(userSelectedName)" />
          </div>
        </v-btn>
      </div>
      <div>
        <p class="result_text font-weight-bold text-center">
          {{ resultTitle }}
        </p>
        <v-btn large class="px-10" @click="playAgain">PLAY AGAIN</v-btn>
      </div>
      <div>
        <p class="pick_title font-weight-bold text-center">THE HOUSE PICKED</p>
        <v-btn
          height="180"
          :style="gradientStyle(botSelectedName)"
          class="circle_button_large"
          disabled
        >
          <div class="circle_button_inner_large" v-if="botSelected">
            <img :src="optionImage(botSelectedName)" />
          </div>
        </v-btn>
      </div>
    </div>
    <Footer />
  </div>
</template>

<script>
import Header from "./Header.vue";
import Footer from "./Footer";
import {
  scissorsStart,
  scissorsEnd,
  paperStart,
  paperEnd,
  rockStart,
  rockEnd,
  lizardStart,
  lizardEnd,
  cyanStart,
  cyanEnd,
} from "../constants/colors";
export default {
  name: "Home",

  components: {
    Header,
    Footer,
  },

  data() {
    return {
      pentagon: require("../../../images/bg-pentagon.svg"),
      scissors: require("../../../images/icon-scissors.svg"),
      paper: require("../../../images/icon-paper.svg"),
      rock: require("../../../images/icon-rock.svg"),
      lizard: require("../../../images/icon-lizard.svg"),
      cyan: require("../../../images/icon-spock.svg"),
      options: ["scissors", "paper", "rock", "lizard", "cyan"],
      winningRules: {
        scissors: ["paper", "lizard"],
        paper: ["rock", "cyan"],
        rock: ["scissors", "lizard"],
        lizard: ["cyan", "paper"],
        cyan: ["scissors", "rock"],
      },
      windowWidth: window.innerWidth,
      userSelected: false,
      userSelectedName: "",
      botSelected: false,
      botSelectedName: "",
      points: 0,
    };
  },

  mounted() {
    window.onresize = () => {
      this.windowWidth = window.innerWidth;
    };
  },

  methods: {
    userPick(name) {
      this.userSelectedName = name;
      this.userSelected = true;
      setTimeout(() => {
        this.botSelectedName =
          this.options[Math.floor(Math.random() * this.options.length)];
        this.botSelected = true;
      }, 1000);
    },
    playAgain() {
      this.userSelected = false;
      this.userSelectedName = "";
      this.botSelected = false;
      this.botSelectedName = "";
    },
    gradientStyle(name) {
      switch (name) {
        case "scissors":
          return {
            background: `linear-gradient(to bottom, ${scissorsStart}, ${scissorsEnd})`,
          };
        case "paper":
          return {
            background: `linear-gradient(to bottom, ${paperStart}, ${paperEnd})`,
          };
        case "rock":
          return {
            background: `linear-gradient(to bottom, ${rockStart}, ${rockEnd})`,
          };
        case "lizard":
          return {
            background: `linear-gradient(to bottom, ${lizardStart}, ${lizardEnd})`,
          };
        case "cyan":
          return {
            background: `linear-gradient(to bottom, ${cyanStart}, ${cyanEnd})`,
          };

        default:
          return {};
      }
    },
    optionImage(name) {
      switch (name) {
        case "scissors":
          return this.scissors;
        case "paper":
          return this.paper;
        case "rock":
          return this.rock;
        case "lizard":
          return this.lizard;
        case "cyan":
          return this.cyan;

        default:
          return this.scissors;
      }
    },
  },

  computed: {
    scissorsStyle() {
      return {
        background: `linear-gradient(to bottom, ${scissorsStart}, ${scissorsEnd})`,
        top: -360 + "px",
      };
    },
    paperStyle() {
      return {
        background: `linear-gradient(to bottom, ${paperStart}, ${paperEnd})`,
        top: -360 + "px",
        left: 130 + "px",
      };
    },
    rockStyle() {
      return {
        background: `linear-gradient(to bottom, ${rockStart}, ${rockEnd})`,
        top: -320 + "px",
        left: 90 + "px",
      };
    },
    lizardStyle() {
      return {
        background: `linear-gradient(to bottom, ${lizardStart}, ${lizardEnd})`,
        top: -440 + "px",
        left: -90 + "px",
      };
    },
    cyanStyle() {
      return {
        background: `linear-gradient(to bottom, ${cyanStart}, ${cyanEnd})`,
        top: -720 + "px",
        left: -130 + "px",
      };
    },
    isWon() {
      if (!this.isDraw) {
        if (
          this.winningRules[this.userSelectedName].includes(
            this.botSelectedName
          )
        ) {
          return true;
        }
      }
      return false;
    },
    isDraw() {
      if (this.botSelected) {
        return this.userSelectedName === this.botSelectedName;
      }
      return true;
    },
    isLose() {
      return !this.isWon && !this.isDraw;
    },
    resultTitle() {
      if (!this.botSelected) {
        return "";
      }
      if (this.isWon) {
        return "YOU WIN";
      }
      if (this.isDraw) {
        return "YOU DRAW";
      }
      return "YOU LOSE";
    },
  },
  watch: {
    isWon(val) {
      if (val) {
        this.points++;
      }
    },
    isLose(val) {
      if (val) {
        this.points--;
      }
    }
  },
};
</script>

<style scoped>
.home-container {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.content {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 100px;
}
.circle_button {
  width: 120px;
  height: 120px;
  border-radius: 60px;
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
}
.circle_button_inner {
  width: 90px;
  height: 90px;
  border-radius: 45px;
  display: flex;
  justify-content: center;
  align-items: center;
  background: white;
}
.circle_button_large {
  width: 180px;
  height: 180px;
  border-radius: 90px;
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 40px;
}
.circle_button_inner_large {
  width: 140px;
  height: 140px;
  border-radius: 70px;
  display: flex;
  justify-content: center;
  align-items: center;
  background: white;
}
.play_mode_container {
  width: 100%;
  max-width: 700px;
  max-height: 200px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 100px;
}
.pick_title {
  font-size: 1.2rem;
  letter-spacing: 0.03125em;
  color: white;
}
.result_text {
  font-size: 2.5rem;
  letter-spacing: 0.03125em;
  color: white;
}
</style>
