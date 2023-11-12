<template>
    <div class="questions-ctr">
        <div class="progress">
            <div class="bar" :style="{
                width:`${questionsAnswered/questions.length*100 }%`
            }"></div>
            <div class="status">
                {{ questionsAnswered }} out of {{ questions.length }} questions answered
            </div>
        </div>

        <transition name="fade">
        <div class="single-question">
            <div class="question">{{ currentQuestion.q }}</div>
            <div class="answers"
              v-for="answer in currentQuestion.answers"
              :key="answer.text"
            >
                <div class="answer" @click.prevent="chooseAnswer(answer)">{{ answer.text }}</div>
            </div>
        </div>
        </transition>
    </div>
  </template>
  
  <script>
  export default {
    name: 'Questions',
    props: ['questionsAnswered', 'questions'],
    emits: ['answer-question'],
    computed: {
        currentQuestion(){
            return this.questions[this.questionsAnswered];
        }
    },
    methods: {
        chooseAnswer(answer){
            this.$emit('answer-question', answer.is_correct);
        }
    }
  }
  </script>
  
  <style>
  
  </style>
  