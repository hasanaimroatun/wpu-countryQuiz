<template>
    <div>
        <div class="card text-center mt-3" :style="{width: '464px', background: 'white'}">
            <div class="card-body">
                <h5 class="card-title">Special title treatment</h5>
                <div class="btnContainer d-flex flex-column gap-4">
                    <button type="button" class="btn btn-outline-secondary text-start" @click="$emit('showResult')">
                        <span>A</span>
                        <span class="me-3"></span>
                    </button>
                    <button type="button" class="btn btn-outline-secondary text-start" @click="$emit('showResult')">
                        <span>B</span>
                        <span class="me-3"></span>
                    </button>
                    <button type="button" class="btn btn-outline-secondary text-start" @click="$emit('showResult')">
                        <span>C</span>
                        <span class="me-3"></span>
                    </button>
                    <button type="button" class="btn btn-outline-secondary text-start" @click="$emit('showResult')">
                        <span>D</span>
                        <span class="me-3"></span>
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Quiz-questions',
        emits: ['showResult']
    }
</script>

<style scoped>
.card-body {
    font-family: 'Poppins', sans-serif;
    padding: 68px 32px;
    box-sizing: border-box;
}

.card-title {
    margin-bottom: 32px;
}

.btn {
    width: 400px;
    height: 56px;
    padding-left: 19px;
}
</style>