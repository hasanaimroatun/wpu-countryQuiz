<template>
    <div>
        <div class="card text-center">
            <div class="card-body">
                <img :src="Logo2" alt="logo2" id="logo2">
                <h5 class="card-title">Results</h5>
                <div class="btnContainer">
                    <div class="result">You got <span>{{getData}}</span> correct answers</div>
                    <button type="button" class="btn" @click="$emit('showQuestions'); reloadPage()">
                        Try again
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Logo2 from '@/assets/undraw_winners_ao2o 2.svg'

    export default {
        name: 'Quiz-result',
        emits: ['showQuestions'],
        setup() {
            return {
                Logo2
            }
        },
        data() {
            let getData = JSON.parse(localStorage.getItem('dataResult'))
            return {
                getData,
            }
        },
        methods: {
            reloadPage() {
                window.location.reload()
            }
        }
    }
</script>

<style scoped>
.card {
    width: 464px;
    background-color: white;
}

.card-body {
    padding: 49px 78px 33px;
    font-family: 'Poppins', sans-serif;
}

#logo2 {
    width: 238px;
}

.card-title {
    font-weight: 700;
    font-size: 48px;
    line-height: 72px;
    margin-top: 52px;
    color: #1D355D;
}

.btnContainer {
    font-weight: 400;
    font-size: 18px;
    line-height: 54px;
    color: #1D355D;
    white-space: nowrap;
    margin-top: -20px;
}

.btnContainer .result span {
    font-weight: 700;
    font-size: 36px;
    color: #6FCF97;
}

.btn {
    padding: 15px 61px;
    margin-top: 51px;
    font-weight: 600;
    font-size: 18px;
    line-height: 27px;
    color: #1D355D;
    border: 1px solid #1D355D;
}

.btn:hover,
.btn:focus {
    background-color: #1D355D;
    color: white;
}

@media screen and (max-width: 576px) {
    .card {
        width: 300px;
    }

    #logo2 {
        width: 200px;
    }

    .card-body {
        padding: 39px 38px 34px;
    }

    .card-title {
        font-size: 35px;
        margin-top: 42px;
    }

    .btnContainer {
        font-size: 15px;
        margin-top: -30px;
    }

    .btnContainer .result span {
        font-size: 28px;
    }

    .btn {
        padding: 10px 51px;
        margin-top: 28px;
        font-size: 15px;
    }
}

</style>