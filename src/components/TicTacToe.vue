<template>
<div>

<span class="repeat" @click="gameRefresh">
  <span class="mdi mdi-refresh" style="font-size: 40px "></span>
</span>
<br>

<div class="center"> 
  <div class="background">
    <div class="wrap">
      <div class="playground" @click="clickEmit(1)">
        <div v-if="target.pl1" >
          <span v-if="target.pl1===1" class="mdi mdi-checkbox-blank-circle-outline" :class="{'red': pl1Red}"></span>
          <span v-if="target.pl1===2" class="mdi mdi-close" :class="{'red': pl1Red}"></span>
        </div>
        <!-- <span class="mdi mdi-close"></span>
        <span class="mdi mdi-checkbox-blank-circle-outline"></span> -->
      </div>
      <div class="playground" @click="clickEmit(2)">
        <div v-if="target.pl2">
          <span v-if="target.pl2===1" class="mdi mdi-checkbox-blank-circle-outline" :class="{'red': pl2Red}"></span>
          <span v-if="target.pl2===2" class="mdi mdi-close" :class="{'red': pl2Red}"></span>
        </div>
      </div>
      <div class="playground" @click="clickEmit(3)">
        <div v-if="target.pl3">
          <span v-if="target.pl3===1" class="mdi mdi-checkbox-blank-circle-outline" :class="{'red': pl3Red}"></span>
          <span v-if="target.pl3===2" class="mdi mdi-close" :class="{'red': pl3Red}"></span>
        </div>
      </div>
    </div>
    <div class="wrap">
      <div class="playground" @click="clickEmit(4)">
        <div v-if="target.pl4">
          <span v-if="target.pl4===1" class="mdi mdi-checkbox-blank-circle-outline" :class="{'red': pl4Red}"></span>
          <span v-if="target.pl4===2" class="mdi mdi-close" :class="{'red': pl4Red}"></span>
        </div>
      </div>
      <div class="playground" @click="clickEmit(5)">
        <div v-if="target.pl5">
          <span v-if="target.pl5===1" class="mdi mdi-checkbox-blank-circle-outline" :class="{'red': pl5Red}"></span>
          <span v-if="target.pl5===2" class="mdi mdi-close" :class="{'red': pl5Red}"></span>
        </div>
      </div>
      <div class="playground" @click="clickEmit(6)">
        <div v-if="target.pl6">
          <span v-if="target.pl6===1" class="mdi mdi-checkbox-blank-circle-outline" :class="{'red': pl6Red}"></span>
          <span v-if="target.pl6===2" class="mdi mdi-close" :class="{'red': pl6Red}"></span>
        </div>
      </div>
    </div>
    <div class="wrap">
      <div class="playground" @click="clickEmit(7)">
        <div v-if="target.pl7">
          <span v-if="target.pl7===1" class="mdi mdi-checkbox-blank-circle-outline" :class="{'red': pl7Red}"></span>
          <span v-if="target.pl7===2" class="mdi mdi-close" :class="{'red': pl7Red}"></span>
        </div>
      </div>
      <div class="playground" @click="clickEmit(8)">
        <div v-if="target.pl8">
          <span v-if="target.pl8===1" class="mdi mdi-checkbox-blank-circle-outline" :class="{'red': pl8Red}"></span>
          <span v-if="target.pl8===2" class="mdi mdi-close" :class="{'red': pl8Red}"></span>
        </div>
      </div>
      <div class="playground" @click="clickEmit(9)">
        <div v-if="target.pl9">
          <span v-if="target.pl9===1" class="mdi mdi-checkbox-blank-circle-outline" :class="{'red': pl9Red}"></span>
          <span v-if="target.pl9===2" class="mdi mdi-close" :class="{'red': pl9Red}"></span>
        </div>
      </div>
    </div>
  </div>
</div>
<div v-if="gameOver" class="footer">
  {{winnerTranslate}}
</div>
</div>
</template>

<script>
import '@mdi/font/css/materialdesignicons.css'
export default {
  name: 'HelloWorld',

  data() {
    return {
      target: {
        pl1: 0,
        pl2: 0,
        pl3: 0,
        pl4: 0,
        pl5: 0,
        pl6: 0,
        pl7: 0,
        pl8: 0,
        pl9: 0
      },
      move: 1,
      gameOver: false,
      winner: 0,
      clickCounter: 0
    }
  },
  computed: {
    winnerTranslate() {
     if(this.winner == 1) return "WINNER IS CIRCLE"
     else if(this.winner == 2) return "WINNER IS X"
     else return "DRAWN GAME"
    }
  },

  methods: {
    changeMove(){
      this.move === 1 ? this.move = 2 : this.move = 1
    },

    clickEmit (pl) {
      if(!this.gameOver){
        let tgName = `pl${pl}`
        if(this.target[tgName] == 0) {
          this.target[tgName] = this.move;
          this.clickCounter++
          this.changeMove()
          if(this.clickCounter == 9) this.gameOverAction(0) 
          this.chooseWinner()
        }
      }
    },

    gameRefresh() {
      for(let i = 1; i <= 9; i++) {
        this.target[`pl${i}`] = 0
        this[`pl${i}Red`] = false
      }
      this.move = 1;
      this.clickCounter = 0;
      this.gameOver = false;
    },

    chooseWinner() {
      let tg = this.target;

      if(tg.pl1 == tg.pl2 && tg.pl2 == tg.pl3 && tg.pl1 != 0) {
        this.pl1Red = true;
        this.pl2Red = true;
        this.pl3Red = true;
        this.gameOverAction(tg.pl1)
      }

      if(tg.pl4 == tg.pl5 && tg.pl5 == tg.pl6 && tg.pl4 != 0) {
        this.pl4Red = true;
        this.pl5Red = true;
        this.pl6Red = true;
        this.gameOverAction(tg.pl4)
      }

      if(tg.pl7 == tg.pl8 && tg.pl8 == tg.pl9 && tg.pl7 != 0) {
        this.pl7Red = true;
        this.pl8Red = true;
        this.pl9Red = true;
        this.gameOverAction(tg.pl7)
      }

      if(tg.pl1 == tg.pl4 && tg.pl4 == tg.pl7 && tg.pl1 != 0) {
        this.pl1Red = true;
        this.pl4Red = true;
        this.pl7Red = true;
        this.gameOverAction(tg.pl1)
      }

      if(tg.pl2 == tg.pl5 && tg.pl5 == tg.pl8 && tg.pl2 != 0) {
        this.pl2Red = true;
        this.pl5Red = true;
        this.pl8Red = true;
        this.gameOverAction(tg.pl2)
      }

      if(tg.pl3 == tg.pl6 && tg.pl6 == tg.pl9 && tg.pl3 != 0) {
        this.pl3Red = true;
        this.pl6Red = true;
        this.pl9Red = true;
        this.gameOverAction(tg.pl3)
      }

      if(tg.pl1 == tg.pl5 && tg.pl5 == tg.pl9 && tg.pl1 != 0){
        this.pl1Red = true;
        this.pl5Red = true;
        this.pl9Red = true;
        this.gameOverAction(tg.pl1)
      }
      if(tg.pl3 == tg.pl5 && tg.pl5 == tg.pl7 && tg.pl3 != 0){
        this.pl3Red = true;
        this.pl5Red = true;
        this.pl7Red = true;
        this.gameOverAction(tg.pl3)
      }

    }, 
    gameOverAction(target) {
      window.console.log(`Winner is ${target}`)
      this.winner = target;
      this.gameOver = true;
    }

    
  }
}
</script>

<style scoped>
* {
  box-sizing: border-box;
}
.center{ 
  display: flex;
  justify-content: center;
  margin-top: 50px;
}
.header{
  margin-top: 20px;
  font-size: 30px;
  color: rgb(99, 0, 0);
}
.background{
  background-image: url("../assets/TicTacBackground.jpg");
  background-repeat: no-repeat; /* Do not repeat the image */
  background-size: cover;
  background-position: center;
  width: 600px;
  height: 600px;
}
.mdi{
  font-size: 170px;
  color: rgb(41, 41, 41);
}
.squere {
  width: 600px;
  height: 600px;
  /* border: 1px solid black; */
}
.wrap{
  display: flex;
}
.playground {
  width: 200px;
  height: 200px;
  /* border: 1px solid black; */
  display: flex;
  justify-content: center;
  align-items: center;
}
.footer{
  margin-top: 50px;
  font-size: 30px;
}
.red{ 
  color: rgb(151, 10, 10);
}
</style>
