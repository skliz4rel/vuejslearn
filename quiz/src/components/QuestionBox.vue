<template>
<div class="question-box-container">
  <b-jumbotron>
       
            <template v-slot:lead>
                    {{ currentQuestion.question }}
            </template>

            <hr class="my-4">
            <b-list-group>
                <b-list-group-item   
                v-for="(answer,index) in answers" 
                :key="index" 
                v-on:click="selectAnswer(index)"
                :class="answerClass(index)"
                 >
                  {{ answer }}
                  </b-list-group-item> 
            </b-list-group>

            <b-button 
            variant="primary"
            v-on:click="submitAnswer"
            :disabled="selectedIndex === null || answered === true"
            >
            Submit
            </b-button>
            <b-button variant="success" href="#" v-on:click="next">Next</b-button>
  </b-jumbotron>
</div>
</template>


<script>
//This script below would allow the variable to be parsed before been displayed into the views. It meant for proper formating
import _ from 'lodash'

export default{

    props:{
        currentQuestion: Object,
        next:Function,
        increment:Function   //This means that this function was passed
    },
    data(){
        return {
            selectedIndex:null,
            shuffledAnswers:[],
            correctIndex:null,
            answered:false
        }
    },
    methods:{
        selectAnswer:function(index){
            this.selectedIndex = index;
        },
        shuffleAnswers:function(){
             let answers = [ ...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer ]
             this.shuffledAnswers= _.shuffle(answers)
             this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer)
        },
        answerClass(index){
            let answerClass= '';

            if(!this.answered &&  this.selectedIndex === index ){
                answerClass = 'selected'
            }
            else if(this.answered && this.correctIndex === index){
                answerClass = 'correct';
            }
            else if(this.answered && this.selectedIndex === index && this.correctIndex !== index){
                answerClass = 'incorrect'
            }

            return answerClass
        },
        submitAnswer:function(){

            let isCorrect = false;

            if(this.selectedIndex === this.correctIndex){
                isCorrect = true;
            }

            this.answered = true;

            this.increment(isCorrect);
        }
    },
    watch:{
      
        currentQuestion:{
            immediate:true,
            handler(){
                this.selectedIndex=null
                this.selectAnswer()
                this.answered = false
            }
        }
    },
    computed:{
    answers:function(){
      let answers = [ ...this.currentQuestion.incorrect_answers ]
      answers.push(this.currentQuestion.currentQuestion)
      return answers;
    }
  }
 
}

</script>


<style scoped>
    .list-group{
        margin-bottom:15px;
    }

    .list-group-item:hover{
        background:#dedede;
        cursor:pointer;
    }

    .btn{
        margin:0 4px;
    }

    .selected{
        background-color:lightblue;
    }

    .correct{
        background-color:lightgreen;
    }

    .incorrect{
        background-color:lightred;
    }
</style>