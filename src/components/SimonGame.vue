<template>
  <div class="panel__container">
    <div class="panel__title">level: {{ level }}</div>
    <div class="panel__row">
      <ColorItem class="panel-bord panel__top-left" :color="'g'" @choose="seleccion"></ColorItem>
      <ColorItem class="panel-bord  panel__top-right" :color="'r'" @choose="seleccion"></ColorItem>
    </div>
    <div class="panel__row">
      <ColorItem class="panel-bord  panel__bottom-left" :color="'y'" @choose="seleccion"></ColorItem>
      <ColorItem class="panel-bord  panel__bottom-right" :color="'b'" @choose="seleccion"></ColorItem>
    </div>
    <div class="panel__center"></div>
    <button class="panel__button" @click="StartGame()" v-if="level === 0">Start Game</button>
  </div>
</template>

<script>
import ColorItem from "@/components/ColorItem.vue";
export default{
  components:{ColorItem},
  data(){
    return { 
      level:0,
      colores:['g','r','y','b'],
      playerSequence:[],
      sequence:[],
      hod:'pc',
      index:0}
  },
  methods:{
    seleccion(data){
      if(this.hod === 'user'){
        this.sequence.push(data);
        this.game();
      }

    },
    game(){
      if( this.sequence[this.index] === this.playerSequence[this.index]){
        this.index++;
        if(this.index === this.level){
          this.sequence = [];
          this.playerSequence = [];
          setTimeout( () => this.StartGame(), 600);
        }
      }
      else{
        alert("Game over");
        this.level = 0;
        this.index = 0;
        this.sequence = [];
        this.playerSequence = [];
        this.hod = 'pc';
      }
    },
    shuffle(){
      return Math.floor(Math.random() * 4);
    },
    StartGame(){
      this.index =0;
      this.hod = 'pc';
      this.level++;
      for(let i = 1; i <= this.level; i++){
        let num = this.colores[this.shuffle()];
        this.playerSequence.push(num);
        setTimeout( () => document.querySelector('#'+num).click(),
        600 * (this.playerSequence.length));
      }
      setTimeout( ()=> this.hod = 'user',600 * (this.playerSequence.length));
    }
  }
}
</script>

<style lang="scss">

.animate__bounceIn{
        opacity: 0.6;
        box-shadow: inset 0px 0px 30px black;
    }
.panel__container {
  border-radius:50px ;
  background: #000;
  padding: 10px;
  width: 450px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 20px;
  position: relative;
}
.panel__title{
  color: #fff;
  position: absolute;
  top: 30%;
  left: 50%;
  transform:translateX(-50%);
  z-index: 3;
}
.panel__row {
  display: flex;
  gap: 20px;
}

.panel__top-left {
  border-top-left-radius: 50%;
  background: red;
}

.panel__top-right {
  border-top-right-radius: 50%;
  background: green;
}

.panel__button{
  position: absolute;
  top: 50%;
  transform: translate(-50%,-50%);
  left: 50%;

  background: #424242;
  border: 1ps solid #fff;
  color: #fff;
  padding: 10px;
}

.panel__bottom-left {
  border-bottom-left-radius: 50%;
  background: blue;
}

.panel__bottom-right {
  border-bottom-right-radius: 50%;
  background: yellow;
}

.panel__center {
  position: absolute;
  width: 300px;
  height: 300px;
  top: 50%;
  transform: translate(-50%,-50%);
    left: 50%;
  background: #000;
  border-radius:50% ;
}

</style>