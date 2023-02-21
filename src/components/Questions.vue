<template>
  <div class="questions-ctr">
    <div class="progress">
      <div
        class="bar"
        :style="{ width: `${(questionsAnswerd / questions.length) * 100}%` }"
      ></div>
      <div class="status">
        {{ questionsAnswerd }} out of {{ questions.length }} questions answered
      </div>
    </div>
    <Transition-group name="fade">
      <div
        class="single-question"
        v-for="(question, qi) in questions"
        :key="question.q"
        v-show="questionsAnswerd === qi"
      >
        <div class="question">
          {{ question.q }}
        </div>

        <div class="answers">
          <div
            class="answer"
            @click.prevent="getAnswerValue(answer.is_correct)"
            v-for="answer in question.answers"
            :key="answer.text"
          >
            {{ answer.text }}
          </div>
        </div>
      </div>
    </Transition-group>
  </div>
</template>

<script>
export default {
  props: ["questions", "questionsAnswerd"],
  data() {
    return {
      emits: ["getAnswer"],
    };
  },
  methods: {
    getAnswerValue(is_correct) {
      this.$emit("getAnswer", is_correct);
    },
  },
};
</script>
