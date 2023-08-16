<template>
  <div class="wrapper-name" :class="{ 'open-name': this.isComplete == true }">
    <div class="name">
      <div class="player">
        <label for="name1">Name Player 1</label>
        <input
          :value="namePlayer[0]"
          @input="changeName1"
          id="name1"
          type="text"
        />
      </div>
      <div class="player">
        <label for="name2">Name Player 2</label>
        <input
          :value="namePlayer[1]"
          @input="changeName2"
          id="name2"
          type="text"
        />
      </div>
      <button @click="complete" class="complete">Bắt đầu</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "PlayersName",
  props: {
    namePlayer: { type: Array, default: [] },
    isComplete: { type: Boolean, default: false }
  },
  data() {
    return {};
  },
  methods: {
    changeName1($event) {
      this.$emit("handleChangeName1", $event);
    },
    changeName2($event) {
      this.$emit("handleChangeName2", $event);
    },
    complete() {
      this.$emit("handleComplete");
    }
  }
};
</script>

<style>
.wrapper-name {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.3);
  visibility: hidden;
  opacity: 0;
  transition: all 0.3s ease;
}

.wrapper-name.open-name {
  opacity: 1;
  visibility: visible;
}

.name {
  width: 450px;
  height: 300px;
  padding: 20px;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%) scale(0.8);
  background: center / cover url('../assets/name.jpg');
  position: absolute;
  font-size: 17px;
  font-family: Arial, Helvetica, sans-serif;
  transition: all 0.3s ease;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.open-name .name {
  transform: translate(-50%, -50%) scale(1);
}
.name input {
  padding: 7px;
  margin: 10px;
  font-size: 15px;
}

.name .complete {
  width: 150px;
  padding: 8px 15px;
  margin-top: 20px;
  font-size: 20px;
  border: 2px solid #333;
  border-radius: 20px;
  background-color: rgba(91, 61, 223, 0.3);
  transition: all 0.3s ease;
}

.name .complete:hover {
  cursor: pointer;
  color: #fff;
  background-color: #100325;
}
</style>
