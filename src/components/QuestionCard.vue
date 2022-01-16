<template>
  <div class="question-card-container mt-2 
">
    <v-card width="400"
elevation="7" outlined  class="mx-auto question-card flex-wrap">
        <v-card-title class="">Questions</v-card-title>
        <v-card-subtitle class="ma-auto">a random quiz</v-card-subtitle>
        <v-card-text>{{currentQuestion.question}} </v-card-text>
        <v-divider class="mx-8"></v-divider>
        <v-list>
      <v-list-item-group  class="justify-content-center"
 >
        <v-list-item
          v-for="(answer,index) in shuffledAnswers" :key="index"
          @click="selectAnswer(index)"
          :class="[answered && correctIndex === index ? 'correct' : '',
          answered && correctIndex != index ? 'incorrect' : '']"
          

        
        >
          <v-list-item-content class="justify-content-center">
            <v-list-item-title v-text="answer"></v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list-item-group>
    </v-list>

        <v-card-actions><v-btn
        color="primary" 
        @click="submitAnswer"
        :disabled="selectedAnswerIndex === null || answered"
>Submit</v-btn> <v-btn color="secondary" @click="next">Next</v-btn></v-card-actions>
    </v-card>

  </div>
</template>

<script>

import shuffle from "lodash/shuffle"

export default {
    props:{
        currentQuestion: Object, //i am receiving this from the parent component
        next: Function,
        increment: Function
        },
        data() {
            return {
                selectedAnswerIndex:null,
                shuffledAnswers:[],
                isCorrect:false,
                answered:false,
                correctIndex:null
            }
        },
        computed:{
            answers(){
                let answers = [...this.currentQuestion.incorrect_answers]
                answers.push(this.currentQuestion.correct_answer)

                return answers
            }
        },
        watch:{ //takes in object or functions and watches for achnges //in my prop and run these functions when there are changes
        currentQuestion:{
            // this.selectedAnswerIndex=null
            // this.shuffleAnswers()
            immediate:true,
            handler() {
            this.selectedAnswerIndex=null 
            this.answered=false
             this.shuffleAnswers()

            }
        }
        },
        methods: {
            selectAnswer(index){
                this.selectedAnswerIndex=index
                console.log(index)
            },
            shuffleAnswers(){
                let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
                this.shuffledAnswers = shuffle(answers)
                this.correctIndex= this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer)

            },
            submitAnswer(){
                this.selectedAnswerIndex === this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer)
 ? this.isCorrect = true : this.isCorrect=false
                this.increment(this.isCorrect)
                this.answered=true
            },
        },
        mounted() {
            this.shuffleAnswers()
        },
}
</script>
<style scoped>
.question-card{
    align-content: center;
}

.correct {
    background-color: rgb(26, 145, 65);
}
.incorrect{
    background-color: rgb(228, 20, 20);
}


</style>
