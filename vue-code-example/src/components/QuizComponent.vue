<template>
  <div class="quiz">
    <div v-if="quizCurrent == 0" class="no-questions">
      start quiz?

      <div @click="changePanel()" class="next-panel">Let's gooooo</div>
    </div>

    <div v-else-if="quizCurrent == 1" class="first-one">
      first question

      <div @click="changePanel()" class="next-panel">Let's gooooo</div>
    </div>

    <div v-else-if="quizCurrent == 2" class="first-one">
      second question

      <div @click="changePanel()" class="next-panel">Let's gooooo</div>
    </div>
    <div v-else-if="quizCurrent == 3" class="first-one">
      third question

      <div @click="changePanel()" class="next-panel">Let's gooooo</div>
    </div>
    <div v-else-if="quizCurrent == 4" class="first-one">
      Your result

      <div @click="changePanel('back')" class="next-panel">
        Back to browsing
      </div>
      <div @click="changePanel('again')" class="next-panel">
        Retake the Quiz
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "QuizComponent",

  data() {
    return {
      quizData: [
        {
          question: "What is the question?",
          answers: {
            option1: {
              text: "I don't know",
              points: 1,
            },
            option2: {
              text: "I do know",
              points: 2,
            },
            option3: {
              text:
                "I am offended by the question and would like to speak to the manager",
              points: 3,
            },
          },
        },
        {
          question: "When is the question?",
          answers: {
            option1: {
              text: "I don't know",
              points: 1,
            },
            option2: {
              text: "I do know",
              points: 2,
            },
            option3: {
              text:
                "I am offended by the question and would like to speak to the manager",
              points: 3,
            },
          },
        },
        {
          question: "Where is the question?",
          answers: {
            option1: {
              text: "I don't know",
              points: 1,
            },
            option2: {
              text: "I do know",
              points: 2,
            },
            option3: {
              text:
                "I am offended by the question and would like to speak to the manager",
              points: 3,
            },
          },
        },
      ],
      quizScore: null,
      quizCurrent: 0,
    };
  },
  methods: {
    changePanel(action) {
      let self = this;
      if (self.quizCurrent == 4 && action == "back") {
        console.log("closing quiz");
      } else if (self.quizCurrent == 4 && action == "again") {
        console.log("retake quiz");
        self.quizCurrent = 0;
      } else {
        console.log("next panel");
        self.quizCurrent += 1;
      }
    },
  },
};
</script>


