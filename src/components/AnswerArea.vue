<template>

<div class="AnswerArea">
    
    <div style="display:flex; height: 35px; width: auto; justify-content: center; align-items: center;">
    <div class="streak animate__animated animate__heartBeat" v-show="streak_val >= 3">
        <span> {{ streak_text }}</span>
        <div class="streak_block" v-bind:class="{low_streak: low_streak, med_streak: med_streak, high_streak: high_streak, legendary_streak:legendary_streak}">{{ streak_val }}</div>
    </div>
    </div>
    
    <div style="margin-top: 30px;">
        <div :key="i.id" v-for="i in numbers">
            <Number :number="i.text" :operation="i.operation" />
        </div>
    </div>

    <AnswerBox @button-clicked="buttonHandler" @new-sesh="createSession" @show-settings="showSettings = true;" @reset-streak="streak_val = 0; low_streak = true; med_streak = false; high_streak = false; legendary_streak = false;" />

    <button @click="buttonHandler(this.correctAnswer)">Answer correctly</button>
</div>


</template>

<script>

import Number from './Number'
import AnswerBox from './AnswerBox'


export default {
    name: 'AnswerArea',
    components: {
        Number,
        AnswerBox
    },
    data() {
        return {
            numbers: [],
            correctAnswer: 0,
            maxDigitsForNumber1: 1,
            maxDigitsForNumber2: 1,
            streak_val: 0,
            low_streak: false,
            med_streak: false,
            high_streak: false,
            legendary_streak: false,
            streak_text: 'Current streak'
        }
    },
    created() {
        this.createSession()
 
    },
    methods: {
            createSession() {
         

            let maxDigitsNumber1 = ""
            let maxDigitsNumber2 = ""

            // Determine the maximum number of digits we can generate
            for(let i=0; i < this.maxDigitsForNumber1; i++) {
                maxDigitsNumber1 += 9
            }

            for(let i=0; i < this.maxDigitsForNumber2; i++) {
                maxDigitsNumber2 += 9
            }


            // Generate the 2 numbers randomly
            let num1 = Math.floor(Math.random() * (parseInt(maxDigitsNumber1)+1))
            let num2 = Math.floor(Math.random() * (parseInt(maxDigitsNumber2)+1))


            // Generate the operation (addition, subtraction, multiplication, division)
            let x = Math.floor(Math.random() * 4)
            let op = ''

            switch(x) {
                case 0: // Addition
                    op = "+"
                    this.correctAnswer = num1 + num2
                    break;
                case 1: // Subtraction
                    op = "-"
                    this.correctAnswer = num1 - num2
                    break;
                case 2: // Multiplication
                    op = "x"
                    this.correctAnswer = num1 * num2
                    break;
                case 3: // Division
                    op = "÷"
                    this.correctAnswer = num1 / num2

                    if(num2 == "0") {this.createSession()}
                    break; 
            }

            if(this.correctAnswer == null || this.correctAnswer == "Infinity") {
                this.createSession()
            }


            // Add new numbers to dict
            this.numbers = [
                {
                    id:1,
                    operation:'',
                    text:num1
                },
                {
                    id:2,
                    operation:op,
                    text:num2
                }
            ]
        },
        buttonHandler(ans) {
            if(ans == this.correctAnswer) {

                let audio = new Audio('correct.mp3');
                audio.loop = false;
                audio.play();
                this.streak_val = this.streak_val + 1
                this.createSession()

                if (this.streak_val >= 3 && this.streak_val < 10) {
                    this.low_streak = true
                    this.streak_text = "Current streak"
                } else if(this.streak_val >= 10 && this.streak_val < 15) {
                    this.med_streak = true
                    this.low_streak = false
                } else if(this.streak_val >= 15 && this.streak_val < 20) {
                    this.high_streak = true
                    this.med_streak = false
                    this.streak_text = "Hot streak"
                } else if(this.streak_val >= 20) {
                    this.legendary_streak = true
                    this.high_streak = false
                    this.streak_text = "Legendary streak"
                }

            }
            else {
             
                this.streak_val = 0
                this.low_streak = true
                this.med_streak = false
                this.high_streak = false
                this.legendary_streak = false
                

            }
        }


    }


}

</script>

<style scoped>

.AnswerArea {
    display: flex;
    flex-direction: column;
    width: 75vw;
    height: 90vh;
    justify-content: center;
}

.streak {
    display:flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    font-size: 1rem;
    font-family: 'Poppins', 'Courier New', Courier, monospace;
    font-weight: 600;
    color: white;
    gap: 10px;
}

button {
    display: block;
    height: 60px;
    width: 100px;
}

.streak_block {
    display: flex;
    border: 1px solid #33cc66; 
    width: 35px;
    height: 35px;
    align-items: center;
    justify-content: center;
    border-radius: 4px;
    background-color: #33cc66;
    font-size: 1.3rem;
    color: black;
}

.low_streak {
    background-color:  	#98fb98;
    border: 1px solid  	#98fb98; 
    color: black;
}

.med_streak {
    background-color: #efd346;
    border: 1px solid #efd346; 
    color: black;
}

.high_streak {
    background-color: #f05338;
    border: 1px solid #f05338; 
    color:white
}

.legendary_streak {
    background-color: #a21abd;
    border: 1px solid #a21abd;
    color:white;
}   



@media only screen and (min-width: 768px) {
    .AnswerArea {
        width: 450px;
    }
} 


</style>