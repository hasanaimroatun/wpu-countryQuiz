<template>
    <div>
        <div class="card text-center mt-3" :style="{width: '464px', background: 'white'}">
            <div class="card-body">
                <h5 class="card-title">Results</h5>
                <div class="btnContainer">
                    <div>You got 4 correct answers</div>
                    <button type="button" class="btn btn-outline-secondary" @click="$emit('showQuestions')">
                        Try again
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Quiz-result',
        emits: ['showQuestions']
    }
</script>

<style scoped>

</style>