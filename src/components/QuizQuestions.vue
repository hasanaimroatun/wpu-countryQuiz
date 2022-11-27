<template>
    <div>
        <div class="card text-center">
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
                <div class="btnContainer d-flex flex-column">
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
                                class="position-absolute end-0 translate-middle iContainer" 
                            />
                        </button> 
                    </div>
                    
                    <div v-show="showNext">
                        <div 
                            class="d-flex justify-content-end nextResultBtnContainer" 
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
import Questions from './questions.json'

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

.btnContainer {
    gap: 23px;
}

.btn {
    width: 400px;
    height: 56px;
    padding-left: 19px;
    color: #6066D0;
    border: 1px solid #6066D0;
    opacity: 70%;
}

.iContainer {
    margin-right: 42px;
    margin-top: 13px;
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

@media screen and (max-width: 576px) {
    .card {
        width: 300px;
    }

    #logo1 {
        left: 200px;
        width: 99px;
    }

    .card-title {
        margin-bottom: 22px;
        font-size: 18px;
    }

    .btnContainer {
        gap: 15px;
    }

    .btn {
        width: 235px;
        height: 43px;
        padding-left: 19px;
    }

    .option {
        font-size: 13px;
    }

    .iContainer {
        margin-top: 10px;
    }

    #btnNextResult {
        padding: 8px 37px;
        font-size: 15px;
    }

    .nextResultBtnContainer {
        width: 235px;
    }
}
</style>