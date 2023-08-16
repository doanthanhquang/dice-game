<template>
  <div class="wrapper-control">
    <button class="control btn-new" @click="newGame">
      <i class="ion-ios-plus-outline"></i>New game
    </button>
    <button class="control btn-roll" @click="rollDice">
      <i class="ion-ios-loop"></i>Roll dice
    </button>
    <button class="control btn-hold" @click="hold">
      <i class="ion-ios-download-outline"></i>Hold
    </button>
    <input
      :disabled="isPlaying"
      :value="finalScore"
      @input="changeFinalScore"
      type="number"
      placeholder="Final score"
      class="final-score"
    />
  </div>
</template>

<script>
export default {
  name: "Control",
  props: {
    finalScore: { type: [Number, String], default: 40 },
    isPlaying: { type: Boolean, default: false }
  },
  data() {
    return {};
  },
  methods: {
    newGame() {
      this.$emit("handleNewGame");
    },
    rollDice() {
      this.$emit("handleRollDice");
    },
    hold() {
      this.$emit("handleHold");
    },
    changeFinalScore($event) {
      this.$emit("handleChangeFinalScore", $event);
    }
  }
};
</script>

<style>
input[type=number]::-webkit-inner-spin-button, 
input[type=number]::-webkit-outer-spin-button { 
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
    margin: 0; 
}
.control {
  position: absolute;
  width: 200px;
  left: 50%;
  transform: translateX(-50%);
  color: #555;
  background: none;
  border: none;
  font-family: Lato;
  font-size: 24px;
  text-transform: uppercase;
  cursor: pointer;
  font-weight: 300;
  transition: background-color 0.3s, color 0.3s;
}
.control.disable {
  pointer-events: none;
}

.control:hover {
  font-weight: 600;
}
.control:hover i {
  margin-right: 20px;
}

.control:focus {
  outline: none;
}

.control i {
  color: #42b983;
  display: inline-block;
  margin-right: 15px;
  font-size: 32px;
  line-height: 1;
  vertical-align: text-top;
  margin-top: -2px;
  transition: margin 0.3s;
}

.btn-new {
  top: 45px;
  font-weight: 600;
}
.btn-roll {
  top: 403px;
  font-weight: 600;
}
.btn-hold {
  top: 467px;
  font-weight: 600;
}

.final-score {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  top: 520px;
  color: #555;
  font-size: 18px;
  font-weight: bold;
  font-family: "Lato";
  text-align: center;
  padding: 10px;
  width: 160px;
  text-transform: uppercase;
}

.final-score:focus {
  outline: none;
}
</style>
