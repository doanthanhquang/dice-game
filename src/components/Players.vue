<template>
  <div class="wrapper-players">
    <!-- player 1 -->
    <div
      class="player-panel"
      v-bind:class="{
        active: activePlayer == 0 && !this.isWinner,
        winner: activePlayer == 0 && this.isWinner
      }"
    >
      <div class="player-name">{{ namePlayer[0] }}</div>
      <div class="player-score">{{ scorePlayer[0] }}</div>
      <div class="player-current-box">
        <div class="player-current-label">Current</div>
        <div class="player-current-score">
          {{ activePlayer == 0 ? currentScore : 0 }}
        </div>
      </div>
    </div>
    <!-- Player 2 -->
    <div
      class="player-panel"
      v-bind:class="{
        active: activePlayer == 1 && !this.isWinner,
        winner: activePlayer == 1 && this.isWinner
      }"
    >
      <div class="player-name">{{ namePlayer[1] }}</div>
      <div class="player-score">{{ scorePlayer[1] }}</div>
      <div class="player-current-box">
        <div class="player-current-label">Current</div>
        <div class="player-current-score">
          {{ activePlayer == 1 ? currentScore : 0 }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Players",
  props: {
    activePlayer: { type: Number, default: 0 },
    scorePlayer: { type: Array, default: [0, 0] },
    currentScore: { type: Number, default: 0 },
    isWinner: { type: Boolean, default: false },
    namePlayer: { type: Array, default: ["", ""] }
  },
  data() {
    return {};
  }
};
</script>

<style>
.player-panel {
  width: 50%;
  float: left;
  height: 600px;
  padding: 100px;
  transition: all 0.3s ease;
  background-color: #fff;
}

.player-name {
  font-size: 40px;
  text-align: center;
  text-transform: uppercase;
  letter-spacing: 2px;
  font-weight: 300;
  margin-top: 20px;
  margin-bottom: 10px;
  position: relative;
}

.player-score {
  text-align: center;
  font-size: 80px;
  font-weight: 300;
  color: #42b983;
  margin-bottom: 130px;
}
.active .player-name{
  font-weight: 600;
}
.active {
  background: center / cover url('../assets/active.jpg');
  color: #42b983;
}

.active .player-name::after {
  content: "\.";
  font-size: 130px;
  position: absolute;
  color: #42b983;
  top: -97px;
  right: 10px;
}

.player-current-box {
  background-color: #42b983;
  color: #fff;
  width: 40%;
  margin: 0 auto;
  padding: 12px;
  text-align: center;
}

.player-current-label {
  text-transform: uppercase;
  margin-bottom: 6px;
  font-weight: 600;
  font-size: 18px;
  color: #333;
}

.player-current-score {
  font-size: 30px;
}

@-webkit-keyframes my {
  0% {
    color: #1b8fc5;
  }
  50% {
    color: #11db33;
  }
  100% {
    color: #1b8fc5;
  }
}
@-moz-keyframes my {
  0% {
    color: #1b8fc5;
  }
  50% {
    color: #11db33;
  }
  100% {
    color: #1b8fc5;
  }
}
@-o-keyframes my {
  0% {
    color: #1b8fc5;
  }
  50% {
    color: #11db33;
  }
  100% {
    color: #1b8fc5;
  }
}
@keyframes my {
  0% {
    color: #1b8fc5;
  }
  50% {
    color: #11db33;
  }
  100% {
    color: #0aadf8;
  }
}
.winner {
  background: #f7f7f7;
}
.winner .player-name {
  font-size: 40px;
  font-weight: 600;
  -webkit-animation: my 700ms infinite;
  -moz-animation: my 700ms infinite;
  -o-animation: my 700ms infinite;
  animation: my 700ms infinite;
}
</style>
