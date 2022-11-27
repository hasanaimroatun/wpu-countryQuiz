<template>
    <div>
        <div class="position-absolute top-50 start-50 translate-middle">
            <div class="text-start" id="title">COUNTRY QUIZ</div>
            <keep-alive>
                <component 
                    :is="activeTab" 
                    :showNext="showNext"
                    class="content" 
                    @showResult='sResult'
                    @showQuestions='sQuestions'
                    @showTrue='sTrueOrFalse($event)'
                />
            </keep-alive>
        </div>
        <div class="createdBy position-absolute bottom-0 start-50 translate-middle-x">
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
               activeTab: 'QuizQuestions',
               showNext: false,
            }
        },
        methods: {
            sResult() {
                this.activeTab = 'QuizResult'
            },
            sQuestions() {
                this.activeTab = 'QuizQuestions'
                this.showNext = false 
            },
            sTrueOrFalse() {
                this.showNext = true
            }
        },
       
    }
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@500;700&family=Poppins:wght@400;500;600;700&display=swap');

#title {
    width: 464px;
    font-family: 'Poppins', sans-serif;
    font-weight: 700;
    font-size: 36px;
    color: #F2F2F2;
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

.createdBy a:hover {
    color: #F9A826;
}
</style>