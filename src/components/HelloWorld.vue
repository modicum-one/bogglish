<template>
  <div class="hello">
    <h1 v-bind:class="{ blinking: timerSeconds==0 }">Bogglish {{timerDisplay}}</h1>
    <button role="button" v-on:click="shake">Shake</button>
    <div class="board">
    <table>
      <tr v-for="(row, indexY) in board" :key="indexY">
        <td v-for="(col, indexX) in row" :key="indexX">
          <div class="cube">{{col}}</div>
        </td>
      </tr>
    </table>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  created: function () {
    this.shake();
    setInterval(()=>{
      this.timerTick();
    },1000)
  },
  methods: {
    shake: function () {
      // console.log("shake it up"+this.board);
      shuffle(this.letterCubes);
      this.board=[];
      for(let i = 0; i<4; i++){
        let row =[];
        for(let j=0;j<4; j++){
          row.push(this.letterCubes[(i*4)+j][0]);
        }
        this.board.push(row);
      }
      this.timerSeconds=180;
      new Audio('./Shake.m4a').play();
    },
    timerTick: function () {
      if(this.timerSeconds > 0) {
        this.timerSeconds--;
        let date = new Date(0);
        date.setSeconds(this.timerSeconds); // specify value for SECONDS here
        this.timerDisplay = date.toISOString().substr(11, 8);
        if (this.timerSeconds == 0){
          new Audio('./awooga-awooga-awooga.mp3').play();
        }
      }
    }
  },
  data: function() {return {
    timeouts:{},
    timerSeconds:0,
    timerDisplay:'',
    letterCubes: [
            ['I','S','P','E','N','H'], //0
            ['F','O','X','I','B','R'], //1
            ['B','I','T','Y','A','L'], //2
            ['D','U','T','N','O','K'], //3
            ['C','A','L','S','E','R'], //4
            ['V','E','N','Z','A','D'], //5
            ['G','E','K','Y','U','L'], //6
            ['P','U','T','L','E','S'], //7
            ['S','O','D','W','E','N'], //8
            ['B','O','M','J','A','Qu'], //9
            ['V','E','G','N','I','T'], //10
            ['L','U','R','W','I','G'], //11
            ['M','E','C','P','A','D'], //12
            ['I','E','H','Y','E','F'], //13
            ['C','O','I','T','A','A'], //14
            ['S','A','M','R','O','H'], //15
    ],
    board:[['','','',''],
           ['','','',''],
           ['','','',''],
           ['','','','']]
  }
  }
}
function shuffle(array) {
  for (let i = array.length - 1; i > 0; i--) {
    let j = Math.floor(Math.random() * (i + 1));
    [array[i], array[j]] = [array[j], array[i]];
    if(Array.isArray(array[i])){
      shuffle(array[i])
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
table{
  margin-left:auto;
  margin-right:auto;
}
div .board{

}
  div .cube{
    font-size: 5rem;
    box-shadow: 5px 5px #888888;
    border:1pt solid black;
    margin:6px;
    width:6rem;
  }

.blinking{
  animation:blinkingText 1.2s infinite;
}
@keyframes blinkingText{
  0%{     color: #F00;    }
  49%{    color: #F00; }
  60%{    color: transparent; }
  99%{    color: transparent;  }
  100%{   color: #F00;    }
}

</style>
