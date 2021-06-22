<template>
  <section class="src-components-cabecera">
    <div id="header" :style="getBackgroundColor">
      <h1>
        {{ titulo }}
        <br />
        <span id="colorDisplay">RGB {{ colorElegido }}</span>
        <br />
        {{ subtitulo }}
      </h1>
    </div>

    <Navbar
      @colorElegidoHeader="setColorElegido($event)"
      @resetearHeader="reset()"
      @colorGanador="mostrarColor()"
    />
  </section>
</template>

<script>
import Navbar from "./Navbar.vue";

export default {
  name: "src-components-cabecera",
  props: [],
  mounted() {},
  components: {
    Navbar,
  },
  data() {
    return {
      titulo: "The Great",
      subtitulo: "Guessing Game",
      colorElegido: null,
      colorBackground: "steelblue",
    };
  },
  methods: {
    setColorElegido(color) {
      this.colorElegido = color;
    },
    mostrarColor() {
      this.colorBackground = this.colorElegido;
    },
    reset() {
      this.colorBackground = null;
    },
  },

  computed: {
    getBackgroundColor() {
      return {
        backgroundColor: this.colorBackground ? this.colorBackground : "steelblue",
      };
    },
  },
};
</script>

<style scoped lang="css">
.src-components-cabecera {
}
#header {
  transition: all 0.3s;
  background: steelblue;
  text-transform: uppercase;
  text-align: center;
  margin: 0;
  color: white;
}
#colorDisplay {
  font-size: 200%;
}
</style>
