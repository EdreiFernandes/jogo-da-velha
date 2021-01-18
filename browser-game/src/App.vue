<template>
  <div id="app">
    <div class="position-absolute d-table w-100 h-100">
        <div class="d-table-cell align-middle">
            <div v-if="playing" id="gameboard" class="container w-board text-center">                
                <app-header :playerTurn="playerTurn"></app-header>

                <div v-for="(gamerow, rowIndex) in gameboard" :key="rowIndex"
                    class="row tiktaktoe">
                    <div v-for="(gamecol, colIndex) in gamerow" :key="colIndex"
                        :class="{'col-4 tiktaktoe-cell text-warning' : true,
                        'tiktaktoe-cell-middle': rowIndex == 1}">
                        <div @click="makeMove(rowIndex, colIndex)" :class="{'empty-cell': gamecol == 'N'}">{{ gamecol }}</div>
                    </div>
                </div>
            </div>

            <div v-else id="menu" class="bg-warning">
                <div class="d-flex justify-content-center">
                    <app-result v-if="showingResult" :result="result" v-on:Close="showScoreboard()"></app-result>
                    <app-scoreboard v-if="showingScore" :player="player" v-on:End="endGame()" v-on:Restart="restartGame()"></app-scoreboard>
                </div>
            </div>
        </div>
    </div>

    <div class="modal fade" data-backdrop="static" id="menuModal" tabindex="-1" role="dialog" aria-labelledby="menuModalLabel"
        aria-hidden="true">
        <div class="modal-dialog modal-dialog-centered" role="document">
            <div class="modal-content bg-warning">
                <div class="row justify-content-center">
                    <div class="col-md-6 col-10">
                        <div class="modal-header">
                            <h5 class="modal-title">Menu</h5>
                            <button type="button" class="close" data-dismiss="modal" aria-label="Close" title="Fechar">
                                <span aria-hidden="true">&times;</span>
                            </button>
                        </div>
                        
                        <div class="modal-body">
                            <button type="button" class="btn btn-outline-dark btn-block" data-dismiss="modal">Jogar</button>
                            <button type="button" class="btn btn-outline-dark btn-block">Reiniciar</button>
                            <button type="button" class="btn btn-outline-dark btn-block" data-dismiss="modal" data-toggle="modal" data-target="#placarModal">
                                Placar
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
  </div>
</template>

<script>
import Header from '@/components/Header.vue';
import Result from '@/components/Result.vue';
import Scoreboard from '@/components/Scoreboard.vue';

export default {
  name: 'App',
  components: {   
      "app-header": Header,
      "app-result": Result,
      "app-scoreboard": Scoreboard,
  },
  data() {
      return {
          playing: true,
          showingResult: false,
          showingScore: false,
          playerTurn: 1,
          result: "Deu velha!",
          gameboard: [
              ['N','N','N'],
              ['N','N','N'],
              ['N','N','N']],
          player: [
              {symbol: 'X', victories: 0},
              {symbol: 'O', victories: 0}],
      }
  },
  methods: {
      makeMove(row, col) {
          if(this.gameboard[row][col] == 'N'){
              this.gameboard[row][col] = this.player[this.playerTurn - 1].symbol;
              if(this.checkVictory()){
                  this.writeScore();
              }else if(this.checkDraw()){
                  this.result = "Deu velha!";
                  this.showResult();
              } else {
                  this.playerTurn = this.playerTurn == 1 ? 2 : 1;
              }
          }
      },
      checkVictory(){
          var hasWon = false;
          for (let index = 0; index < 3; index++) {
              // check row
              if(this.gameboard[index][0] != 'N' && this.gameboard[index][1] != 'N' && this.gameboard[index][2] != 'N'){
                  hasWon = this.gameboard[index][0] == this.gameboard[index][1] && this.gameboard[index][1] == this.gameboard[index][2];
                  if(hasWon) return true;
              }

              // check column
              if(this.gameboard[0][index] != 'N' && this.gameboard[1][index] != 'N' && this.gameboard[2][index] != 'N'){
                  hasWon = this.gameboard[0][index] == this.gameboard[1][index] && this.gameboard[1][index] == this.gameboard[2][index];
                  if(hasWon) return true;
              }
          }

          if(this.gameboard[1][1] != 'N'){
              // check diagonal
              if(this.gameboard[2][2] != 'N' && this.gameboard[0][0] != 'N'){
                  hasWon = this.gameboard[0][0] == this.gameboard[1][1] && this.gameboard[1][1] == this.gameboard[2][2];
                  if(hasWon) return true;
              }

              // check inverted diagonal
              if(this.gameboard[0][2] != 'N' && this.gameboard[2][0] != 'N'){
                  hasWon = this.gameboard[0][2] == this.gameboard[1][1] && this.gameboard[1][1] == this.gameboard[2][0];
                  if(hasWon) return true;
              }
          }          
          return false;
      },
      checkDraw(){
          var emptyCells = 0;
          for (let row = 0; row < 3; row++) {
              for (let col = 0; col < 3; col++) {
                  if(this.gameboard[row][col] == 'N') emptyCells++;
              }
          }

          return emptyCells == 0;
      },
      writeScore(){
          this.result = "O Jogador " + this.playerTurn + " venceu!";
          this.player[this.playerTurn - 1].victories++;
          this.showResult();
      },
      restartGame(){
          this.playerTurn = 1,
          this.gameboard = [
              ['N','N','N'],
              ['N','N','N'],
              ['N','N','N']];
          this.hideMenu();
      },
      endGame(){
          this.player = [
              {symbol: 'X', victories: 0},
              {symbol: 'O', victories: 0}];
          this.result = "Obrigado por jogar";
          this.showResult();
      },
      showResult(){
          this.showingResult = true;
          this.showingScore = false;
          this.playing = false;
      },
      showScoreboard(){
          this.showingResult = false;
          this.showingScore = true;
          this.playing = false;
      },
      hideMenu(){
          this.showingResult = false;
          this.showingScore = false;
          this.playing = true;
      }
  },
}
</script>

<style>
.w-board {
  width: 45%;
}

.tiktaktoe {
  font-size: 6rem;
}

.tiktaktoe .tiktaktoe-cell:nth-of-type(2) {
  border-right: solid 3px;
  border-left: solid 3px;
}

.tiktaktoe .tiktaktoe-cell-middle {
  border-top: solid 3px;
  border-bottom: solid 3px;
}

.tiktaktoe .tiktaktoe-cell:hover {
  background-color: #2a2e33;
}

.empty-cell{
    color: #2a2e3300;
}

@media only screen and (max-width: 600px) {
  .w-board {
    width: 90%;
  }
  .tiktaktoe {
    font-size: 3rem;
  }
}
</style>
