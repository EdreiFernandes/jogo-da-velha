<template>
    <div id="cabealho" class="row justify-content-between mb-5">
        <a class="text-warning" data-toggle="modal" data-target="#placarModal" title="Placar">
            <i class="fas fa-trophy"></i>
        </a>
        <div class="text-warning">vez do<h2><b>Jogador {{ playerTurn }}</b></h2></div>
        <a class="text-warning" data-toggle="modal" data-target="#menuModal" title="Menu">
            <i class="fas fa-ellipsis-v"></i>
        </a>
    </div>
</template>

<script>
    export default {
        props: {
            playerTurn: {
                type: Number,
                default: 0
            },
        },
    }
</script>