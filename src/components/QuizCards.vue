<template>
    <div>
        <div class="position-absolute top-50 start-50 translate-middle">
            <div class="text-start" :style="{width: '464px'}">COUNTRY QUIZ</div>
            
            <keep-alive>
                <component :is="activeTab" class="content" :activeTab='activeTab'/>
            </keep-alive>
        </div>
        <div class="createdBy mb-4 position-absolute bottom-0 start-50 translate-middle-x">
            created by <a href="https://github.com/hasanaimroatun/wpu-countryQuiz">hasanaimroatun</a> - devChallenges.io
        </div>
    </div>
</template>

<script>
import QuizQuestions from './QuizQuestions.vue'
import QuizResult from './QuizResult.vue'

    export default {
        name: 'Quiz-card',
        components: {
            QuizQuestions,
            QuizResult,
        },
        data() {
            return {
               activeTab: 'QuizQuestions' 
            }
        }
    }
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@500;700&family=Poppins:wght@400;500;600;700&display=swap');

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

.createdBy {
    font-family: 'Montserrat', sans-serif;
    font-size: 14px;
    line-height: 17.07px;
    font-weight: 500;
    color: #F2F2F2;
}

.createdBy a {
    color: inherit;
    text-decoration: none;
    font-weight: 700;
}
</style>