<template>
  <div class="questions-ctr">
    <div class="progress">
      <div
        class="bar"
        :style="{ width: `${(questionsAnswered / questions.length) * 100}%` }"
      ></div>
      <div class="status">
        {{ questionsAnswered }} out of {{ questions.length }} questions answered
      </div>
    </div>
    <transition-group name="fade">
      <div
        class="single-question"
        v-for="(question, qi) in questions"
        :key="question.q"
        v-show="questionsAnswered === qi"
      >
        <div class="question">{{ question.q }}</div>
        <div class="answers">
          <div
            class="answer"
            v-for="answer in question.answers"
            :key="answer.text"
            @click.prevent="selectAnswer(answer.is_correct)"
          >
            {{ answer.text }}
          </div>
        </div>
      </div>
    </transition-group>
  </div>
</template>

<script>
  export default {
    name: 'Questions',

    props: {
      questions: {
        type: Array,
        required: true
      },
      questionsAnswered: {
        type: Number,
        required: true
      }
    },

    emits: ['answer-answered'],

    methods: {
      selectAnswer(is_correct) {
        this.$emit('answer-answered', is_correct)
      }
    }
  }
</script>

<style scoped>
  .bar {
    height: 50px;
    background-color: #ff6372;
    transition: all .3s linear;
  }
</style>