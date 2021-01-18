<template>
    <div class="modal fade" data-backdrop="static" id="scoreboardModal" tabindex="-1" role="dialog"
        aria-labelledby="scoreboardModalLabel" aria-hidden="true">
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
                                    <h1>{{ player[0].victories }}</h1>
                                    <h6>vitórias</h6>
                                </div>
                                <h2 class="col-2 mt-5"><b>X</b></h2>
                                <div id="jogador-2" class="col-5">
                                    <h4>Jogador 2</h4>
                                    <h1>{{ player[1].victories }}</h1>
                                    <h6>vitórias</h6>
                                </div>
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
        props: {
            player: {
                type: Array
            },
        },
    }
</script>
