<template>
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
                            <button type="button" class="btn btn-outline-dark btn-block" data-dismiss="modal" @click="restart()">Reiniciar</button>
                            <button type="button" class="btn btn-outline-dark btn-block" data-dismiss="modal" data-toggle="modal" data-target="#scoreboardModal">
                                Placar
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        methods: {
            restart(){
                this.$emit("Restart");
            }
        }, 
    }
</script>