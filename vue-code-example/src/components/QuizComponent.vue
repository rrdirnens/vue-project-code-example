<template>
  <div class="quiz">
    <div v-if="quizPanelCurrent == 0" class="quiz__panel quiz__start">
      <div class="quiz__start-opening-text">
        We've prepared a short quiz for you, which will let you know your
        earning potential for your property. Would you like to proceed?
      </div>

      <div @click="changePanel()" class="quiz__next">Let's go</div>
    </div>

    <div
      v-for="(question, index) in quizData"
      :key="index"
      class="quiz__question-wrapper"
      v-show="quizPanelCurrent == index + 1"
    >
      <div
        v-if="quizPanelCurrent == index + 1"
        class="quiz__panel quiz__question"
      >
      <div class="quiz__tracking">
        <div class="quiz__progress-percent">{{ progress }}%</div>
        <div class="quiz__progress-tracker">
          <div
            class="quiz__progress-progress"
            :style="{ width: userProgress + '%' }"
          ></div>
        </div>
      </div>
        <div class="quiz__question-text">{{ question.question }}</div>
        <div class="quiz__question-answers">
          <div
            v-for="(answer, index) in question.answers"
            :key="index"
            @click="updateScore(answer.points, $event)"
            class="quiz__question-answer"
          >
            <div class="quiz__question-answer-text">
              {{ answer.text }}
            </div>
          </div>
        </div>

        <div @click="changePanel()" class="quiz__next">Next question</div>
      </div>
    </div>

    <div v-if="finished" class="quiz__panel quiz__finish">
      <div class="quiz__tracking">
        <div class="quiz__progress-percent">{{ progress }}%</div>
        <div class="quiz__progress-tracker">
          <div
            class="quiz__progress-progress"
            :style="{ width: userProgress + '%' }"
          ></div>
        </div>
      </div>
      <div class="quiz__thanks">You're all done! Thanks for participating.</div>

      <div v-if="quizScore >= 0 && quizScore < 10" class="quiz__finish-message">
        Your score is {{ quizScore }}, which means you're a bit of a dummy
      </div>
      <div
        v-else-if="quizScore >= 10 && quizScore < 25"
        class="quiz__finish-message"
      >
        Your score is {{ quizScore }}, which means you're not entirely stupid
      </div>
      <div
        v-else-if="quizScore >= 25 && quizScore < 50"
        class="quiz__finish-message"
      >
        Your score is {{ quizScore }}, which means you're almost intelligent
      </div>
      <div
        v-else-if="quizScore >= 50 && quizScore < 75"
        class="quiz__finish-message"
      >
        Your score is {{ quizScore }}, which means you're probably not exactly a
        rocket scientist, but among the other dummies, you're doing pretty good
        and should be proud of yourself. Like the r-worded kid they bring out
        during half time, to shoot a three-pointer.
      </div>

      <div class="quiz__finish-options">
        <div
          @click="changePanel('back')"
          class="quiz__finish-option quiz__close"
        >
          Back to browsing
        </div>
        <div
          @click="changePanel('again')"
          class="quiz__finish-option quiz__retake"
        >
          Retake the Quiz
        </div>
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
          question: "How many pets do you have on your property?",
          answers: {
            option1: {
              text: "None",
              points: 50,
            },
            option2: {
              text: "1-5",
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
      ],
      quizScore: null,
      quizScoreCurrent: null,
      quizPanelCurrent: 0,
      finished: false,
      userProgress: 0,
    };
  },
  methods: {
    //Runs when user clicks "Next Question"
    changePanel(action) {
      let self = this;
      let last =
        self.quizData.lastIndexOf(self.quizData[self.quizData.length - 1]) + 2;
      let oneBeforeLast = last - 1;

      //Check if the panel being closed is the last question
      if (self.quizPanelCurrent == oneBeforeLast) {
        self.finished = true;
      } else {
        self.finished = false;
      }

      //Check if it's the closing quiz panel AND the user selects the "Back to browsing"
      if (self.quizPanelCurrent == last && action == "back") {
        // console.log('backk')
        self.quizScore = null;
        self.quizScoreCurrent = null;

        //Check if it's the closing quiz panel AND the user selects the "Retake the quiz"
      } else if (self.quizPanelCurrent == last && action == "again") {
        // console.log('againn')
        self.quizPanelCurrent = 0;
        self.quizScore = null;
        self.quizScoreCurrent = null;

        //Run this when the user submits and answer
      } else {
        self.quizPanelCurrent += 1;
        self.quizScore += self.quizScoreCurrent;
        self.quizScoreCurrent = null;
      }
    },
    updateScore(points, event) {
      //Run every time an answer is selected, but not submitted

      let answers = document.querySelectorAll(".quiz__question-answer");
      let target = event.currentTarget;
      let targetClass = "quiz__question-answer--selected";

      //Loop through all answers and remove the '--selected' modifier
      answers.forEach((a) => {
        a.classList.remove(targetClass);
      });

      //Add the '--selected' modifier to the selected answer
      target.classList.add(targetClass);

      //Check if a score for the current question has been registered.
      //If it's not registered, the just add the score
      if (this.quizScoreCurrent == null) {
        this.quizScoreCurrent += points;

        //If it is registered, clear the score and then add the score
      } else {
        this.quizScoreCurrent = null;
        this.quizScoreCurrent += points;
      }
    },
  },
  computed: {
    progress() {
      //Run this on every panel to keep track of user's progress through the quiz
      let totalLength = this.quizData.length;
      let current = this.quizPanelCurrent - 1;
      let endValue = Math.round((current / totalLength) * 100);

      //We don't want the percentage to ever be shown as below zero, so we change it to zero
      if (endValue <= 0) {
        endValue = 0;
      }

      //Save value and return to frontend
      this.userProgress = endValue;
      return this.userProgress;
    },
  },
};
</script>