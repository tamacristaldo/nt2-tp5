<template>
  <section class="src-components-contenedor">
    <div id="container">
      <div class="squares">
        <Cuadrado
          v-for="(color, i) in colors"
          :key="i"
          :color="colors[i]" 
          :pos="i"         
          @clickSquare="clickSquare($event)" 
        />
        
      </div>
    </div>
  </section>
</template>

<script>
import Cuadrado from "./Cuadrado.vue";
export default {
  name: "src-components-contenedor",
  props: ["isHard"],
  beforeMount() {
    this.$parent.$on("resetear", this.changeData);
  },
  mounted() {
    this.init();
  },
  components: {
    Cuadrado,
  },

  data() {
    return {
      colors: [],
      pickedColor: "",
      ItIsHard: true,
    };
  },
  methods: {
    init() {
      this.colors = this.createNewColors(this.ItIsHard);
      this.pickedColor = this.colors[this.pickColor()];
      this.$emit("colorElegido", this.pickedColor);
    },
    pickColor() {
      var quantity;
      if (this.ItIsHard) {
        quantity = 6;
      } else {
        quantity = 3;
      }
      return Math.floor(Math.random() * quantity);
    },
    createNewColors(bool) {
      let numbers = bool ? 6 : 3;
      var arr = [];
      for (var i = 0; i < numbers; i++) {
        arr.push(this.createRandomStringColor());
      }
      return arr;
    },
    changeData(estado) {
      this.ItIsHard = estado;
      this.init();
    },
    createRandomStringColor() {
      var newColor =
        "rgb(" +
        this.randomInt() +
        ", " +
        this.randomInt() +
        ", " +
        this.randomInt() +
        ")";
      return newColor;
    },
    randomInt() {
      return Math.floor(Math.random() * 256);
    },
    clickSquare(color) {
      if (color[0] == this.pickedColor) {
        this.$emit("colorGanador");
        this.colors = this.colors.map(() => {
          return this.pickedColor;
        });
      } else {
        this.$emit("colorPerdedor");
        this.colors.splice([color[1]], 1, "#232323");
      }
    },
  },
  computed: {},
};
</script>

<style scoped lang="css">
#container {
  margin: 20px auto;
  max-width: 600px;
}
</style>
