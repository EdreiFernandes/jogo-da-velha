<template>
    <div id="result" class="row col-sm-7 my-5 justify-content-between">
        <h2 class="col-10 text-center">{{ result }}</h2>

        <button type="buttom" class="btn btn-warning col-1" @click="close()">
            <i class="fas fa-times"></i>
        </button>
    </div>
</template>

<script>
    export default {
        props: {
            result: {
                type: String,
                default: ""
            },
        },
        methods: {
            close() {
                this.$emit("Close");
            }
        },
    }
</script>