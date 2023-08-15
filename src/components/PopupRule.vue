<template>
  <div class="wrapper-popup" :class="{ 'open-popup': isPopup }">
    <div class="rule">
      <h3>Luật chơi</h3>
      <ol>
        <li>
          Người chơi tiến hành đổ xúc xắc, tổng số điểm quay được sẽ tạm lưu vào
          current.
        </li>
        <li>
          Nếu người chơi đổ trúng số 1 thì sẽ bị reset điểm current về 0 và
          chuyển lượt chơi.
        </li>
        <li>Nếu người chơi muốn lưu điểm lại thì ấn Hold.</li>
        <li>
          Người chơi nào đạt được mốc Final Score trước sẽ là người chiến thắng.
        </li>
      </ol>
      <button @click="confirm" class="confirm">Đã hiểu</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "PopupRule",
  props: {
    isPopup: { type: Boolean, default: false }
  },
  data() {
    return {};
  },
  methods: {
    confirm() {
      this.$emit("handleConfirm");
    }
  }
};
</script>

<style>
.wrapper-popup {
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

.wrapper-popup.open-popup {
  opacity: 1;
  visibility: visible;
}
.rule {
  width: 450px;
  padding: 20px;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%) scale(0.8);
  background: center / cover url('../assets/rule.jpg');
  color: #333;
  position: absolute;
  font-family: Arial, Helvetica, sans-serif;
  transition: all 0.3s ease;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.rule h3 {
  margin-bottom: 10px;
}
.rule ol {
  padding-left: 20px;
}
.open-popup .rule {
  transform: translate(-50%, -50%) scale(1);
}
.rule .confirm {
  width: 150px;
  padding: 8px 15px;
  margin-top: 20px;
  font-size: 20px;
  border: 2px solid #333;
  border-radius: 20px;
  background-color: rgba(91, 61, 223, 0.3);
  transition: all 0.3s ease;
}

.rule .confirm:hover {
  cursor: pointer;
  color: #fff;
  background-color: #100325;
}
</style>
