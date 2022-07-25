<template>

<div v-if="showSettings">
    <Settings @close-event="showSettings = false"/>
</div>


<input type="text" v-model="answer" @input="inputHandler" id="answerInputBox" v-on:keyup.enter="forward" v-on:keyup.r="$emit('new-sesh')" autofocus />
<div style="display: flex; justify-content: space-between;">
    <div style="display: flex; flex-direction: row; gap: 7px;">
        <button class="settingsButton" @click="showSettings = true"><img src="../../public/settings_FILL1_wght200_GRAD0_opsz48.svg" alt=""></button>
        <button class="refreshButton" @click="$emit('new-sesh'); $emit('reset-streak')"><img src="../../public/refresh_FILL0_wght600_GRAD0_opsz48.svg" alt=""></button>
    </div>
            <transition name="easeIn">
                <button id="nextQuest" v-show="inputNotEmpty" @click="forward"><img src="../../public/chevron_right_FILL1_wght700_GRAD0_opsz48.svg" alt=""></button>
            </transition>
    </div>

</template>
<script>

import Settings from "./Settings.vue"

export default {
    name: 'AnswerBox',
    components: { Settings,},
    data() {
        return {
            inputNotEmpty: false,
            showSettings: false
        }
    },
    methods: {
        inputHandler() {
            const inpField = document.getElementById('answerInputBox')

            if(inpField.value.slice(-1) == "r") {
                inpField.value = "";
                this.answer = "";
                this.inputNotEmpty = false

                this.$emit('reset-streak')
            }

            if(this.answer.length != 0) {
                this.inputNotEmpty = true

            } else {
                this.inputNotEmpty = false 
            }
        },
        forward() {
            this.$emit('button-clicked', this.answer)
            
            const inpField = document.getElementById('answerInputBox')
            inpField.value = "";
            this.answer = "";

            this.inputNotEmpty = false;


            
        },
        closeSettings() { 
            this.showSettings = false 
            }

    }
}

</script>

<style scoped>

input {
    display: flex;
    background: none;
    justify-content: flex-end;
    border: none;
    color: white;
    font-family: 'Poppins', 'Courier New', Courier, monospace;
    font-weight: 600;
    outline: none;
    font-size:3.5rem;
    width: auto;
    height: 65px;
    text-align: right;
    
}

button {
    display: flex;
    border-radius: 20%;
    height: 50px;
    width: 50px;
    background: none;
    border: 1px solid  	 	 	 	 	#85e9fa;
    background-color:  	 	 	 	 	#85e9fa;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    margin-top: 10px;
}

button:active {
    animation: forwards 0.3s float;
}

.refreshButton {
    border: 1px solid  	 	#85e88d;
    background-color:  	 	#85e88d;
}

.settingsButton {
    border: 1px solid  	 	 	 	#f97ac4;
    background-color:  	 	 	 	#f97ac4;
}


img {
    height: 32px;
    width: 32px;
}

.easeIn-enter-active {
    animation: forwards 0.4s easeIn;
}

.easeIn-leave-active {
    animation: forwards 0.4s easeOut;
}

@keyframes easeIn {
    0% {
        opacity: 0;
        transform: translateY(-80%);
    }
    20% {
        opacity: 0;
    }
    50% {
        opacity: 1;
        transform: translateY(0%);
    }
    100% {
        opacity: 1;
        transform: translateY(0%);
    }
}

@keyframes easeOut {
    0% {
        opacity: 1;
        transform: translateX(0%);
    }
    20% {
        opacity: 1;
    }
    50% {
        opacity: 0;
        transform: translateY(-80%);
    }
    100% {
        opacity: 0;
        transform: translateY(-80%);
    }
}

@keyframes float {
    0% {
        transform: translateY(0%);
    }
    40% {
        transform: translateY(-20%);
    }
    100% {
        transform: translateY(0%);
    }
}


</style>