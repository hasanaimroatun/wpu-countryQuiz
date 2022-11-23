<template>
    <div>
        <div class="card text-center mt-3" :style="{width: '464px', background: 'white'}">
            <div class="card-body">
                <h5 class="card-title">Special title treatment</h5>
                <div class="btnContainer">
                    Result
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Quiz-result',
        props: ['activeTab']
    }
</script>

<style scoped>

</style>