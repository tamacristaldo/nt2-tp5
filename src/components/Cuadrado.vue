<template>
  <section class="src-components-cuadrado">
    <div class="square" :style="{ background: color }" @click="clickSquare()"></div>
  </section>
</template>

<script lang="js">

  export default  {
    name: 'src-components-cuadrado',
    props: ['color','pos'],
    mounted () {

    },
    data () {
      return {
      }
    },
    methods: {
      clickSquare(){
        this.$emit('clickSquare',[this.color,this.pos])
      }
    },
    computed: {

    }
}


</script>

<style scoped lang="css">
.src-components-cuadrado {
}
.square {
	width: 30%;
	background: blue;
	padding-bottom: 30%;
	float: left;
	margin: 1.66%;
	border-radius: 10%;
	transition: background 0.8s;
	-webkit-transition: background 0.8s;
	-moz-transition: background 0.8s;
}
</style>
