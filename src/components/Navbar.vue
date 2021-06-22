<template>
  <section class="src-components-nabvar">
    <div id="navigator">
      <button id="reset" @click="resetear()">{{ textContent }}</button>
      <span id="message"> {{ messageDisplay }}</span>

      <button id="easy" :class="!isHard && 'selected'" @click="changeToEasy()">easy</button>

      <button id="hard" :class="isHard && 'selected'" @click="changeToHard()">hard</button>
      <Contenedor
        :isHard="isHard"
        @colorElegido="setColorElegido($event)"
        @colorGanador="showWinnerMessage()"
        @colorPerdedor="showLoserMessage()"
      />
    </div>
  </section>
</template>

<script>
import Contenedor from "./Contenedor.vue";
export default {
  name: "src-components-nabvar",
  components: {
    Contenedor,
  },
  props: [],
  mounted() {},
  data() {
    return {
      isHard: true,
      colorElegido: "",
      messageDisplay: "",
      textContent: "New Colors!",
    };
  },
  methods: {
    changeToEasy() {
      if (this.isHard) {
        this.isHard = false;
        this.resetear();
      }
    },
    changeToHard() {
      if (!this.isHard) {
        this.isHard = true;
        this.resetear();
      }
    },
    resetear() {
      this.textContent = "New Colors!";
      this.$emit("resetear", this.isHard);
      this.$emit("resetearHeader");
    },
    setColorElegido(color) {
      this.$emit("colorElegidoHeader", color);
    },
    showWinnerMessage() {
      this.messageDisplay = "You Picked Right!";
       this.textContent = "Play Again!";
      this.$emit("colorGanador");
    },
    showLoserMessage() {
      this.messageDisplay = "Try Again!";
    },
  },
  computed: {},
};
</script>

<style scoped lang="css">
#navigator {
  background: #ffffff;
  height: 30px;
  text-align: center;
  margin: 0;
  margin-top: -30px;
}
#message {
  color: #000000;
  display: inline-block;
  width: 20%;
}
button {
  border: none;
  background-color: white;
  font-family: "Montserrat", "Avenir";
  text-transform: uppercase;
  height: 100%;
  font-weight: 700;
  letter-spacing: 1px;
  color: steelblue;
  transition: all 0.3s;
  outline: none;
}
button:hover {
  color: white;
  background-color: steelblue;
}
.selected {
  background-color: steelblue;
  color: white;
}
</style>
