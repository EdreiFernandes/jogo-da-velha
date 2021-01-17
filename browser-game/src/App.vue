<template>
  <div id="app">
    <div class="position-absolute d-table w-100 h-100">
        <div class="d-table-cell align-middle">
            <div v-if="playing" id="gameboard" class="container w-board text-center">                
                <Header :playerTurn="playerTurn"></Header>

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
                    <div class="row col-sm-7 my-5 justify-content-between">
                        <h2 class="col-10 text-center">{{ result }}</h2>

                        <button type="buttom" class="btn btn-warning col-1" @click="hideMenu()">
                            <i class="fas fa-times"></i>
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <div class="modal fade" data-backdrop="static" id="placarModal" tabindex="-1" role="dialog"
        aria-labelledby="placarModalLabel" aria-hidden="true">
        <div class="modal-dialog modal-dialog-centered" role="document">
            <div class="modal-content bg-warning">
                <div class="row justify-content-center">
                    <div class="col-md-6 col-10">
                        <div class="modal-header">
                            <h5 class="modal-title">Placar</h5>
                            <button type="button" class="close" data-dismiss="modal" aria-label="Close" title="Fechar">
                                <span aria-hidden="true">&times;</span>
                            </button>
                        </div>
    
                        <div class="modal-body">
                            <div class="row text-center">
                                <div id="jogador-1" class="col-5">
                                    <h4>Jogador 1</h4>
                                    <h1>4</h1>
                                    <h6>vitórias</h6>
                                </div>
                                <h2 class="col-2 mt-5"><b>X</b></h2>
                                <div id="jogador-2" class="col-5">
                                    <h4>Jogador 2</h4>
                                    <h1>2</h1>
                                    <h6>vitórias</h6>
                                </div>
                            </div>
                        </div>
                    </div>
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

export default {
  name: 'App',
  components: {   
      Header 
  },
  data() {
      return {
          playing: false,
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
                  this.result = "Player " + this.playerTurn + " ganhou!";
                  this.showMenu();
              }else if(this.checkDraw()){
                  this.result = "Deu velha!";
                  this.showMenu();
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

          if(this.gameboard[0][0] != 'N' && this.gameboard[1][1] != 'N'){
              // check diagonal
              if(this.gameboard[2][2] != 'N'){
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
      showMenu(){
          this.playing = false;
      },
      hideMenu(){
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
