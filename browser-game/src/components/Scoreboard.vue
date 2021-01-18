<template>
    <div id="scoreboard" class="row col-sm-7 my-4 text-center">
        <div id="player-1" class="col-5">
            <h4>Jogador 1</h4>
            <h1>{{ player[0].victories }}</h1>
            <h6>vitórias</h6>
        </div>

        <h2 class="col-2 mt-5"><b>X</b></h2>

        <div id="player-2" class="col-5">
            <h4>Jogador 2</h4>
            <h1>{{ player[1].victories }}</h1>
            <h6>vitórias</h6>
        </div>

        <div class="d-flex col-12 mt-4 justify-content-between">
            <button type="button" class="btn btn-outline-danger col-5" @click="end()">Encerrar</button>
            <button type="button" class="btn btn-outline-dark col-5" @click="restart()">Reiniciar</button>
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
        methods: {
            end() {
                this.$emit("End");
            },
            restart(){
                this.$emit("Restart");
            }
        },
    }
</script>

<style lang="scss" scoped>

</style>