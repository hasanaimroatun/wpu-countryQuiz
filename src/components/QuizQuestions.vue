<template>
    <div>
        <div class="card text-center" :style="{width: '464px', background: 'white'}">
            <div class="card-body" :style="paddingStyle">
                <img :src="Logo1" alt="logo1" id="logo1">
                <div v-show="Questions[indx].picURL">
                    <img 
                        :src="Questions[indx].picURL" 
                        alt="image" 
                        :style="{width: '80px', marginTop: '-32px', marginLeft: '72px'}" 
                        class="position-absolute start-0 translate-middle"
                    >
                </div>
                <h5 class="card-title text-start">{{Questions[indx].question}}</h5> 
                <div class="btnContainer d-flex flex-column gap-4">
                    <div v-for="(opt, index) in ['A', 'B', 'C', 'D']" :key="opt">
                        <button 
                            type="button" 
                            class="btn text-start option" 
                            @click="$emit('showTrue'); showTOrF($event)"
                            @mouseenter="over($event)"
                            @mouseleave="out($event)"
                        >
                            {{opt}} 
                            <span>{{Questions[indx].options[index]}}</span> 
                            <span 
                                class="position-absolute end-0 translate-middle" 
                                :style="{marginRight: '42px', marginTop: '13px'}"
                            />
                        </button> 
                    </div>
                    
                    <div v-show="showNext">
                        <div 
                            class="d-flex justify-content-end" 
                            :style="{width: '400px'}" 
                            @click="bNextOrResult($event)"
                        >
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
                                    @click="$emit('showResult'); bgDefault(); clearResult()"
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
                isQuestion: true,
                result: 0,
            }
        },
        mounted() {
            // axios
            // .get('https://restcountries.com/v3.1/name/sweden')
            // .then((response) => {
            //     console.log(response.data)
            // })
            // .catch((err) => {
            //     console.log(err.message)
            // })
            
        },
        updated() {
            if(this.showNext === true) {
                this.paddingStyle.padding = '68px 32px 18px'
            } else {
                this.paddingStyle.padding = '68px 32px'
            }
        },
        setup() {
            return {
                Logo1
            }
        },
        methods: {
            saveToLocal() {
                localStorage.setItem('dataResult', JSON.stringify(this.result))
            },
            bNextOrResult(e) {
                if(e.currentTarget.textContent === 'Next') {
                    this.indx += 1
                } else {
                    this.indx -= (this.Questions.length - 1)
                }
            },
            showTOrF(e) {
                const bOption = document.querySelectorAll('.option')
                
                for(let i = 0; i < bOption.length; i++) {
                    if(bOption[i].childNodes[1].textContent === this.Questions[this.indx].answer) {
                        Object.assign(bOption[i].style, {backgroundColor: '#60BF88', border: '1px solid #60BF88', color: 'white'})
                        let icn = document.createElement("i")
                        icn.classList.add('fa-regular')
                        icn.classList.add('fa-circle-check')

                        if(bOption[i].childNodes[2].childNodes.length === 0) {
                            bOption[i].childNodes[2].append(icn)
                        }
                    }
                    bOption[i].style.opacity = '1'
                }

                if(e.currentTarget.childNodes[1].textContent !== this.Questions[this.indx].answer){
                    console.log(false)
    
                    if(e.target.classList.contains('btn')) {
                        Object.assign(e.target.style, {backgroundColor: '#EA8282', border: '1px solid #EA8282', color: 'white'})
                    } else {
                        Object.assign(e.target.parentElement.style, {backgroundColor: '#EA8282', border: '1px solid #EA8282', color: 'white'})
                    }
                    
                    let icn = document.createElement("i")
                    icn.classList.add('fa-regular')
                    icn.classList.add('fa-circle-xmark')

                    if(e.target.classList.contains('btn')) {
                        e.target.childNodes[2].append(icn)
                    } else {
                        e.target.nextSibling.append(icn)
                    }
                }
                
                if (e.currentTarget.childNodes[1].textContent === this.Questions[this.indx].answer) {
                    this.result += 1
                }

                this.isQuestion = false
                
            },
            clearIcon() {
                const bOption = document.querySelectorAll('.option')
                for(let i = 0; i < bOption.length; i++) {
                    if(bOption[i].childNodes[2].childNodes.length !== 0) {
                        bOption[i].childNodes[2].childNodes[0].remove()
                    }
                }
            },
            bgDefault() {
                const bOption = document.querySelectorAll('.option')
                for(let i = 0; i < bOption.length; i++) {
                    Object.assign(bOption[i].style, {backgroundColor: 'white', border: '1px solid #6066D0', color: '#6066D0', opacity: '70%'})
                    
                    if(bOption[i].childNodes[2].childNodes.length !== 0) {
                        bOption[i].childNodes[2].childNodes[0].remove()
                    }
                }

                setTimeout(() => {
                    this.clearIcon()
                }, 200)

                this.isQuestion = true

            },
            clearResult() {
                this.saveToLocal()
                this.result = 0

                // setTimeout(() => {
                //     this.result = 0
                // }, 200)
            },
            over(e) {
                if(this.isQuestion === true) {
                    Object.assign(e.target.style, {backgroundColor: '#F9A826', border: '1px solid #F9A826', color: 'white', opacity: '1'})
                }
            },
            out(e) {
                if(this.isQuestion === true) {
                    Object.assign(e.target.style, {backgroundColor: 'white', border: '1px solid #6066D0', color: '#6066D0', opacity: '70%'})
                }
            },
            // getScore() {
            //     this.$emit('clicked', this.result)
            // }
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

#btnNextResult {
    font-weight: 700;
    width: fit-content;
    padding: 15px 47px;
    color: white;
    background-color: #F9A826;
    border: 1px solid #F9A826;
    opacity: 1;
}

#btnNextResult:hover {
    background-color: #ff771d;
    border: 1px solid #ff771d;
}
</style>