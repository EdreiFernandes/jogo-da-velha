<template>
  <div id="app">
    <div class="position-absolute d-table w-100 h-100">
        <div class="d-table-cell align-middle">
            <div class="container w-board text-center">
                <div id="cabealho" class="row justify-content-between mb-5">
                    <a class="text-warning" data-toggle="modal" data-target="#placarModal" title="Placar">
                        <i class="fas fa-trophy"></i>
                    </a>
                    <div class="text-warning">vez do<h2><b>Jogador {{ playerTurn }}</b></h2></div>
                    <a class="text-warning" data-toggle="modal" data-target="#menuModal" title="Menu">
                        <i class="fas fa-ellipsis-v"></i>
                    </a>
                </div>

                <div v-for="(gamerow, rowIndex) in gameboard" :key="rowIndex"
                    class="row tiktaktoe">
                    <div v-for="(gamecol, colIndex) in gamerow" :key="colIndex"
                        :class="{'col-4 tiktaktoe-cell text-warning' : true,
                        'tiktaktoe-cell-middle': rowIndex == 1}">
                        <div>N</div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <div class="modal fade" data-backdrop="static" id="resultadoModal" tabindex="-1" role="dialog"
        aria-labelledby="resultadoModalLabel" aria-hidden="true">
        <div class="modal-dialog modal-dialog-centered" role="document">
            <div class="modal-content bg-warning">
                <div class="row justify-content-center">
                    <div class="col-md-6 col-10">
                        <div class="modal-header">
                            <button type="button" class="close" data-dismiss="modal" aria-label="Close" title="Fechar">
                                <span aria-hidden="true">&times;</span>
                            </button>
                        </div>
    
                        <div class="modal-body text-center">
                            <h2>Deu velha!</h2>
                        </div>
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
export default {
  name: 'App',
  components: {    
  },
  data() {
      return {
          playerTurn: 1,

          //   player: [{id: 1, symbol: 'X', victories: 0},{id: 1, symbol: 'O', victories: 0}],
      gameboard: [
          ['N','N','N'],
          ['N','N','N'],
          ['N','N','N']]
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

.modal-dialog {
  margin: 0;
  max-width: 100%;
}

.modal-content {
  border: none;
  border-radius: 0px;
}

.modal-header {
  border: none;
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
