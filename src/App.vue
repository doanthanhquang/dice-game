<template>
  <div id="app">
    <div class="wrapper clearfix">
      <Players
        :isWinner="isWinner"
        :activePlayer="activePlayer"
        :scorePlayer="scorePlayer"
        :currentScore="currentScore"
        :namePlayer="namePlayer"
      />
      <Control
        :isPlaying="isPlaying"
        :finalScore="finalScore"
        @handleNewGame="handleNewGame"
        @handleRollDice="handleRollDice"
        @handleHold="handleHold"
        @handleChangeFinalScore="handleChangeFinalScore"
      />
      <Dices :dices="dices" />
      <PopupRule :isPopup="isPopup" @handleConfirm="handleConfirm" />
      <PopupWinner
        :namePlayer="namePlayer"
        :scorePlayer="scorePlayer"
        :isPopupWiner="isPopupWiner"
        :isWinner="isWinner"
        :activePlayer="activePlayer"
        @handleClose="handleClose"
      />
      <PlayersName
        :namePlayer="namePlayer"
        :isComplete="isComplete"
        @handleChangeName1="handleChangeName1"
        @handleChangeName2="handleChangeName2"
        @handleComplete="handleComplete"
      />
    </div>
  </div>
</template>

<script>
import Players from "./components/Players.vue";
import Control from "./components/Control.vue";
import Dices from "./components/Dices.vue";
import PopupRule from "./components/PopupRule.vue";
import PopupWinner from "./components/PopupWinner.vue";
import PlayersName from "./components/PlayersName.vue";

export default {
  name: "app",
  components: {
    Players,
    Control,
    Dices,
    PopupRule,
    PopupWinner,
    PlayersName
  },
  data() {
    return {
      isPlaying: false,
      isPopup: false,
      activePlayer: 0,
      scorePlayer: [0, 0],
      dices: [2, 3],
      namePlayer: ["Player 1", "Player 2"],
      currentScore: 0,
      finalScore: 10,
      isPopupWiner: false,
      isComplete: false
    };
  },
  methods: {
    nextPlayer() {
      this.activePlayer = this.activePlayer === 0 ? 1 : 0;
      this.currentScore = 0;
    },
    handleNewGame() {
      this.isPopup = true;
    },
    handleConfirm() {
      this.isPopup = false;
      this.isComplete = true;
    },
    handleComplete() {
      this.isComplete = false;
      this.activePlayer = 0;
      this.isPlaying = true;
      this.scorePlayer = [0, 0];
      this.dices = [1, 1];
      this.currentScore = 0;
    },
    handleRollDice() {
      if (this.isPlaying) {
        var dice1 = Math.ceil(Math.random() * 6);
        var dice2 = Math.ceil(Math.random() * 6);
        let activePlayer = this.activePlayer;

        this.dices = [dice1, dice2];
        if (dice1 === 1 || dice2 === 1) {
          setTimeout(() => {
            alert(`${this.namePlayer[activePlayer]} đổ trúng số 1. Rất tiếc!`);
            this.nextPlayer();
          }, 300);
        } else {
          this.currentScore = this.currentScore + dice1 + dice2;
        }
      } else {
        alert("Vui lòng ấn New Game");
      }
    },
    handleHold() {
      if (this.isPlaying) {
        let { scorePlayer, activePlayer, currentScore } = this;

        this.$set(
          this.scorePlayer,
          activePlayer,
          scorePlayer[activePlayer] + currentScore
        );

        if (!this.isWinner) {
          this.nextPlayer();
        } else {
          this.isPopupWiner = true;
        }
      } else {
        alert("Vui lòng ấn New Game");
      }
    },
    handleChangeFinalScore(e) {
      var number = parseInt(e.target.value);
      if (isNaN(number)) {
        this.finalScore = "";
      } else {
        this.finalScore = number;
      }
    },
    handleChangeName1(e) {
      this.namePlayer = [e.target.value, this.namePlayer[1]];
    },
    handleChangeName2(e) {
      this.namePlayer = [this.namePlayer[0], e.target.value];
    },
    handleClose() {
      this.isPopupWiner = false;
    }
  },
  computed: {
    isWinner() {
      let { scorePlayer, finalScore } = this;
      if (scorePlayer[0] >= finalScore || scorePlayer[1] >= finalScore) {
        this.isPlaying = false;
        return true;
      }
      return false;
    }
  }
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

.clearfix::after {
  content: "";
  display: table;
  clear: both;
}

body {
  background: center / cover url(./assets/back.jpg),
    linear-gradient(rgba(62, 20, 20, 0.4), rgba(62, 20, 20, 0.4));
  font-family: Lato;
  font-weight: 300;
  position: relative;
  height: 100vh;
  color: #555;
}

.wrapper {
  width: 1000px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: #fff;
  box-shadow: 0px 10px 50px rgba(0, 0, 0, 0.3);
  overflow: hidden;
}
</style>
