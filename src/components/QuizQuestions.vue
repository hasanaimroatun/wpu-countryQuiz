<template>
    <div>
        <div class="card text-center" :style="{width: '464px', background: 'white'}">
            <div class="card-body" :style="paddingStyle">
                <img :src="Logo1" alt="logo1" id="logo1">
                <div v-show="Questions[indx].picURL">
                    <img :src="Questions[indx].picURL" alt="image" :style="{width: '80px', marginTop: '-32px', marginLeft: '72px'}" class="position-absolute start-0 translate-middle">
                </div>
                <h5 class="card-title text-start">{{Questions[indx].question}}</h5> 
                <div class="btnContainer d-flex flex-column gap-4">
                    <!-- <button type="button" class="btn text-start" @click="$emit('showTrue')">
                        <span>A</span>
                        <span :style="{marginLeft: '15px'}">{{Questions[qIndex].options.a}}</span>
                    </button>
                    <button type="button" class="btn text-start" @click="$emit('showTrue')">
                        <span>B</span>
                        <span :style="{marginLeft: '15px'}">{{Questions[qIndex].options.b}}</span>
                    </button>
                    <button type="button" class="btn text-start" @click="$emit('showTrue')">
                        <span>C</span>
                        <span :style="{marginLeft: '15px'}">{{Questions[qIndex].options.c}}</span>
                    </button>
                    <button type="button" class="btn text-start" @click="$emit('showTrue')">
                        <span>D</span>
                        <span :style="{marginLeft: '15px'}">{{Questions[qIndex].options.d}}</span>
                    </button> -->
                    <div v-for="(opt, index) in ['A', 'B', 'C', 'D']" :key="opt">
                        <button 
                            type="button" 
                            class="btn text-start option" 
                            @click="$emit('showTrue'); showTOrF($event)"
                        >
                            {{opt}} <span>{{Questions[indx].options[index]}}</span> 
                        </button> 
                    </div>
                    
                    <div v-show="showNext">
                        <div class="d-flex justify-content-end" :style="{width: '400px'}" @click="bNextOrResult($event)">
                            <div v-if="this.indx < Questions.length - 1">
                                <button 
                                    type="button" 
                                    class="btn text-start" 
                                    id="btnNextResult" 
                                    @click="$emit('showQuestion'); bgDefault()"
                                    v-text="stringBtn"
                                >
                        
                                </button>
                            </div>
                            <div v-else-if="this.indx === Questions.length - 1">
                                <button 
                                    type="button" 
                                    class="btn text-start" 
                                    id="btnNextResult" 
                                    @click="$emit('showResult'); bgDefault()"
                                >
                                    Total Result
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Logo1 from '@/assets/undraw_adventure_4hum 1.svg'
// import axios from 'axios'
import Questions from './questions.json'
// import { reactive, toRefs } from 'vue'

    export default {
        name: 'Quiz-questions',
        emits: ['showQuestion', 'showTrue', 'showResult'],
        props: {
            showNext: {
                type: Boolean,
                required: true
            }
        },
        data() {
            return {
                paddingStyle: {
                    padding: '68px 32px'
                },
                Questions,
                indx: 0,
                stringBtn: 'Next',
            }
        },
        // mounted() {
        //     axios
        //     .get('https://restcountries.com/v3.1/name/sweden')
        //     .then((response) => {
        //         console.log(response.data)
        //     })
        //     .catch((err) => {
        //         console.log(err.message)
        //     })
        // },
        updated() {
            if(this.showNext === true) {
                this.paddingStyle.padding = '68px 32px 18px'
            } else {
                this.paddingStyle.padding = '68px 32px'
            }

            // if(this.qIndex === this.Questions.length - 1) {
            //     this.btnString = 'Result'
            // } else {
            //     this.btnString = 'Next'
            // }

            // const buttonString = document.getElementById('btnNextResult').textContent
            // console.log(buttonString)
            
        },
        setup() {
            return {
                Logo1
            }
        },
        methods: {
            bNextOrResult(e) {
                // if(e.currentTarget.textContent === 'Next') {
                //     this.indx += 1
                // } else {
                //     this.indx -= (this.Questions.length - 1)
                // }

                if(e.currentTarget.textContent === 'Next') {
                    this.indx += 1
                } else {
                    this.indx -= (this.Questions.length - 1)
                }
            },
            showTOrF(e) {
                // if(e.currentTarget.childNodes[1].textContent === this.Questions[this.indx].answer){
                //     console.log(true)
                //     e.target.style.backgroundColor = '#60BF88'
                //     e.target.style.border = '1px solid #60BF88'
                //     e.target.style.color = 'white'
                // } else {
                //     console.log(false) 
                //     e.target.style.backgroundColor = '#EA8282'
                //     e.target.style.border = '1px solid #EA8282'
                //     e.target.style.color = 'white'
                // }

                const bOption = document.querySelectorAll('.option')
                for(let i = 0; i < bOption.length; i++) {
                    if(bOption[i].childNodes[1].textContent === this.Questions[this.indx].answer) {
                        bOption[i].style.backgroundColor = '#60BF88'
                        bOption[i].style.border = '1px solid #60BF88'
                        bOption[i].style.color = 'white'
                    }
                    bOption[i].style.opacity = '1'
                }

                if(e.currentTarget.childNodes[1].textContent !== this.Questions[this.indx].answer){
                    console.log(false)
                    e.target.style.backgroundColor = '#EA8282'
                    e.target.style.border = '1px solid #EA8282'
                    e.target.style.color = 'white'
                }
            },
            bgDefault() {
                const bOption = document.querySelectorAll('.option')
                for(let i = 0; i < bOption.length; i++) {
                    bOption[i].style.backgroundColor = 'white'
                    bOption[i].style.border = '1px solid #6066D0'
                    bOption[i].style.color = '#6066D0'
                    bOption[i].style.opacity = '70%'
                }
            },
            bgFocusHover() {
                const bOption = document.querySelectorAll('.option')
                for(let i = 0; i < bOption.length; i++) {
                    bOption[i].style.backgroundColor = '#F9A826'
                    bOption[i].style.border = '1px solid #F9A826'
                    bOption[i].style.color = '#white'
                    bOption[i].style.opacity = '1'
                }
            }
        }
    }
</script>

<style scoped>
.card-body {
    font-family: 'Poppins', sans-serif;
    box-sizing: border-box;
}

#logo1 {
    position: absolute;
    top: -55px;
    left: 346px;
    width: 117px;
}

.card-title {
    margin-bottom: 32px;
}

.btn {
    width: 400px;
    height: 56px;
    padding-left: 19px;
    color: #6066D0;
    border: 1px solid #6066D0;
    opacity: 70%;
}

.btn:hover,
.btn:focus,
#btnNextResult {
    color: white;
    background-color: #F9A826;
    border: 1px solid #F9A826;
    opacity: 1;
}

#btnNextResult {
    font-weight: 700;
    width: fit-content;
    padding: 15px 47px;
}
</style>