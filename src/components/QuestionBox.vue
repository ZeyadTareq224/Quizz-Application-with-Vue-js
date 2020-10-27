<template>
  <div class="col-6 offset-3">
    <div class="jumbotron">
        <h1 class="display-4">{{currentQuestion.category}} </h1>
        <p class="lead">{{currentQuestion.question}}</p>
        <span class="badge badge-warning"><h6>{{currentQuestion.difficulty}}</h6></span>
        <hr class="my-4">
        <ul class="list-group mb-5">
            <li :class="answerClass(index)"
            @click="selectAnswer(index)" v-for="(shuffledAnswer, index) in shuffledAnswers" :key=index class="list-group-item">{{ shuffledAnswer }}</li>
        </ul>
        
        <button :disabled="selectedIndex === null || answered" 
        @click="submitAnswer" 
        class="btn btn-primary btn-lg mr-1 ml-1" 
        role="button"
        >
        Submit
        </button>
        <a class="btn btn-success btn-lg mr-1 ml-1" href="#" role="button" @click="next">Next</a>
    </div>
  </div>
</template>

<script>
import _ from 'lodash'
export default {
    name: "QuestionBox",
    props:{
        currentQuestion: Object,
        next: Function,
        increment: Function
    },
    data(){
        return {
            selectedIndex: null,
            correctIndex:null,
            shuffledAnswers: [],
            answered: false,
        }
    },
    watch:{
        currentQuestion(){
            this.selectedIndex = null
            this.shuffleAnswers()
            this.answered = false
        }
    },
    computed: {
        answers(){
            let answers = [...this.currentQuestion.incorrect_answers]
            answers.push(this.currentQuestion.correct_answer)
            return answers
        }
    },
    mounted(){
        this.shuffleAnswers()
    },
    methods: {
        selectAnswer(index){
            this.selectedIndex = index
        },
        shuffleAnswers(){
            let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
            this.shuffledAnswers = _.shuffle(answers)
            this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer)
        },
        submitAnswer(){
            let isCorrect = false
            if (this.selectedIndex === this.correctIndex){
                isCorrect = true
            }
            this.answered = true
            this.increment(isCorrect)
        },
        answerClass(index){
            let answerClass = ''
            if(!this.answered && this.selectedIndex === index){
                answerClass = 'selected'
            }else if(this.answered && this.correctIndex === index){
                answerClass = 'correct'
            }else if (this.answered && this.selectedIndex === index && this.correctIndex !== index){
                answerClass = 'incorrect'
            }else{
                answerClass = ''
            }
            return answerClass

        }
    }
} 
</script>

<style scoped>
    .list-group-item:hover {
        background: #EEE;
        cursor: pointer;
    }

    .selected {
        background: rgb(136, 201, 223);
    }
    .correct {
        background: lightgreen;
    }
    .incorrect {
        background: red;
    }

</style>

