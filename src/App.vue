<template>
  <div class="ctr">
    <transition name="fade" mode="out-in">
    <questions v-if="questionsAnswered < questions.length"
      :questionsAnswered="questionsAnswered"
      :questions="questions"
      @answer-question="answerQuestion"
    />
    <result v-else :result="result"/>
  </transition>
  <button type="button" class="reset-btn" @click.prevent="reset">Reset</button>
</div>
</template>

<script>
import Questions from '@/components/Questions.vue'
import Result from '@/components/Result.vue'

export default {
  name: 'App',
  components:{
    Questions,
    Result
  },
  data() {
    return {
      questionsAnswered: 0,
      score: 0,
      result: {},
      questions: [
        {
            q: 'What is 2 + 2?', 
            answers: [
                {
                    text: '4',
                    is_correct: true
                },
                {
                    text: '3',
                    is_correct: false 
                },
                {
                    text: 'Fish',
                    is_correct: false 
                },
                {
                    text: '5',
                    is_correct: false 
                }
            ] 
        },
        { 
            q: 'How many letters are in the word "Banana"?', 
            answers: [
                {
                    text: '5',
                    is_correct: false
                },
                {
                    text: '7',
                    is_correct: false 
                },
                {
                    text: '6',
                    is_correct: true 
                },
                {
                    text: '12',
                    is_correct: false 
                }
            ] 
        },
        { 
            q: 'Find the missing letter: C_ke', 
            answers: [
                {
                    text: 'e',
                    is_correct: false
                },
                {
                    text: 'a',
                    is_correct: true 
                },
                {
                    text: 'i',
                    is_correct: false 
                }
            ] 
        },
      ], 
      results: [
        {
            min: 0,
            max: 2,
            title: "Try again!",
            desc: "Do a little more studying and you may succeed!"
        },
        {
            min: 3,
            max: 3,
            title: "Wow, you're a genius!",
            desc: "Studying has definitely paid off for you!"
        }
      ]
    }
  },
  methods: {
    answerQuestion(answer){
      if (answer) this.score++;
      this.questionsAnswered++;

      if (this.questionsAnswered == this.questions.length) {
        this.result = this.results.find(
          elem => elem.min <= this.score && this.score <= elem.max
        )
      }
    },
    reset(){
      this.score = 0;
      this.questionsAnswered = 0;
    }
  },
}
</script>

<style>

</style>
