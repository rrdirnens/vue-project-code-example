<template>
  <div class="quiz">
    <div v-if="quizPanelCurrent == 0" class="no-questions">
      start quiz?

      <div @click="changePanel()" class="next-panel">Let's gooooo</div>
    </div>

    <div v-for="(question, index) in quizData" :key="index" class="quiz-wrapper">
      <div v-if="quizPanelCurrent == index + 1" class="first-one">
        {{index + 1}}st question:

        <div class="question-text">{{question.question}}</div>
        <div class="answers">
          <div v-for="(answer, index) in question.answers" :key="index" @click="updateScore(answer.points)" class="answer">
            {{answer.text}}
            {{answer.points}}
          </div>
        </div>

        <div @click="changePanel()" class="next-panel">Let's gooooo</div>
      </div>
    </div>

    <div v-if="finished" class="fourth-one">
      Your result: {{quizScore}}

      What does your score mean? 
      0-5 points is excellent
      5-30 points is good 
      30-45 points means you're r-worded

      <div v-if="quizScore > 5" class="">your score is over five which means you are not r-worded</div>

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
        }
      ],
      quizScore: null,
      quizScoreCurrent: null,
      quizPanelCurrent: 0,
      finished: false
    };
  },
  methods: {

    //Runs when user clicks "Next Question"
    changePanel(action) {
      let self = this;
      let last = self.quizData.lastIndexOf(self.quizData[self.quizData.length - 1]) + 2
      let oneBeforeLast = last - 1
    
      //Check if the panel being closed is the last question
      if (self.quizPanelCurrent == oneBeforeLast) {
        self.finished = true
      } else {
        self.finished = false
      }

      //Check if it's the closing quiz panel AND the user selects the "Back to browsing"
      if (self.quizPanelCurrent == last && action == 'back') {
        // console.log('backk')
        self.quizScore = null
        self.quizScoreCurrent = null

      //Check if it's the closing quiz panel AND the user selects the "Retake the quiz"
      } else if (self.quizPanelCurrent == last && action == 'again') {
        // console.log('againn')
        self.quizPanelCurrent = 0
        self.quizScore = null
        self.quizScoreCurrent = null

      //Run this when the user submits and answer
      } else {
        self.quizPanelCurrent += 1
        self.quizScore += self.quizScoreCurrent
        self.quizScoreCurrent = null
      }
    },
    updateScore(points) {

      //Run every time an answer is selected, but not submitted
      //Check if a score for the current question has been registered.
      //If it's not registered, the just add the score
      if (this.quizScoreCurrent == null) {
        this.quizScoreCurrent += points

      //If it is registered, clear the score and then add the score
      } else {
        this.quizScoreCurrent = null
        this.quizScoreCurrent += points
      }
    }
  },
};
</script>