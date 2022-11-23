<template>
    <div>
        <div class="card text-center" :style="{width: '464px', background: 'white'}">
            <div class="card-body" :style="paddingStyle">
                <img :src="Logo1" alt="logo1" id="logo1">
                <h5 class="card-title">Special title treatment</h5>
                <div class="btnContainer d-flex flex-column gap-4">
                    <button type="button" class="btn text-start" @click="$emit('showTrue')">
                        <span>A</span>
                        <span class="me-3"></span>
                    </button>
                    <button type="button" class="btn text-start" @click="$emit('showTrue')">
                        <span>B</span>
                        <span class="me-3"></span>
                    </button>
                    <button type="button" class="btn text-start" @click="$emit('showTrue')">
                        <span>C</span>
                        <span class="me-3"></span>
                    </button>
                    <button type="button" class="btn text-start" @click="$emit('showTrue')">
                        <span>D</span>
                        <span class="me-3"></span>
                    </button>
                    <div v-show="showNext">
                        <div class="d-flex justify-content-end" :style="{width: '400px'}">
                            <button 
                                type="button" 
                                class="btn text-start" 
                                id="btnNext" 
                                @click="$emit('showResult')"
                            >
                                Next
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Logo1 from '@/assets/undraw_adventure_4hum 1.svg'

    export default {
        name: 'Quiz-questions',
        emits: ['showResult', 'showTrue'],
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
#btnNext {
    color: white;
    background-color: #F9A826;
    border: 1px solid #F9A826;
    opacity: 1;
}

#btnNext {
    font-weight: 700;
    width: fit-content;
    padding: 15px 47px;
}
</style>