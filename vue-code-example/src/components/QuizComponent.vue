<template>
  <div class="magic" v-show="!showQuiz">
    <div class="button button__magic" @click="showQuiz = true">Show me the magic</div>
  </div>
  <div class="quiz" v-show="showQuiz">
    <div v-if="quizPanelCurrent == 0" class="quiz__panel quiz__start">
      <div class="quiz__start-opening-text">
        We've prepared a short quiz for you, which will let you know your
        earning potential for your property. Would you like to proceed?
      </div>

      <div @click="changePanel()" class="quiz__start-button">Let's go</div>
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

      <div v-if="quizScore >= 0 && quizScore < 15" class="quiz__finish-message">
        Your score is {{ quizScore }}. This is pretty low and we would recommend to get your score up to at least 15 if you want to make a competitive profit.
      </div>
      <div
        v-else-if="quizScore >= 15 && quizScore < 30"
        class="quiz__finish-message"
      >
        Your score is {{ quizScore }}. This score means that you can are going to make an average amount of profit. Try to get your score up to 30-40 if you want to make the most out of your property.
      </div>
      <div
        v-else-if="quizScore >= 30 && quizScore <= 40"
        class="quiz__finish-message"
      >
        Your score is {{ quizScore }}. Congrats, you are in a good position to make the most profit out of your property.
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
      showQuiz: false,
      quizData: [
        {
          question: "How many pets do you have on your property?",
          answers: {
            option1: {
              text: "None",
              points: 5,
            },
            option2: {
              text: "I have 1-3 pets",
              points: 2,
            },
            option3: {
              text:
                "I have more than 3 pets",
              points: 0,
            },
          },
        },
        {
          question: "How many months of the year is your property available?",
          answers: {
            option1: {
              text: "10-12 months",
              points: 5,
            },
            option2: {
              text: "3-10 months",
              points: 2,
            },
            option3: {
              text:
                "Less than 3 months",
              points: 0,
            },
          },
        },
        {
          question: "What's the average lowest temperature where your property is located?",
          answers: {
            option1: {
              text: "It's ever below freezing",
              points: 5,
            },
            option2: {
              text: "A little below freezing",
              points: 2,
            },
            option3: {
              text:
                "Unbearable level of cold",
              points: 0,
            },
          },
        },
        {
          question: "How many separate bedrooms does your property have?",
          answers: {
            option1: {
              text: "More than 5",
              points: 5,
            },
            option2: {
              text: "Between 2-5",
              points: 2,
            },
            option3: {
              text:
                "1",
              points: 0,
            },
          },
        },
        {
          question: "How many bathrooms does your property have per bedroom?",
          answers: {
            option1: {
              text: "1 or more",
              points: 5,
            },
            option2: {
              text: "Less than 1 but more than 0.5",
              points: 2,
            },
            option3: {
              text:
                "Less than 0.5",
              points: 0,
            },
          },
        },
        {
          question: "What's the average hottest temperature where your property is located?",
          answers: {
            option1: {
              text: "Higher than 30 degrees Celsius",
              points: 5,
            },
            option2: {
              text: "Between 20 and 30 degrees Celsius",
              points: 2,
            },
            option3: {
              text:
                "Less than 20 degrees Celsius",
              points: 0,
            },
          },
        },
        {
          question: "Does your property have heating and hot water?",
          answers: {
            option1: {
              text: "Yes to both",
              points: 5,
            },
            option2: {
              text: "Has heating but no hot water",
              points: 2,
            },
            option3: {
              text:
                "Has hot water, but no heating",
              points: 0,
            },
          },
        },
        {
          question: "Does your property have free Wi-Fi for tennants?",
          answers: {
            option1: {
              text: "Yes",
              points: 5,
            },
            option2: {
              text: "No",
              points: 0,
            }
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
        self.quizPanelCurrent = 0
        self.showQuiz = false
        self.quizScore = null
        self.quizScoreCurrent = null

        //Check if it's the closing quiz panel AND the user selects the "Retake the quiz"
      } else if (self.quizPanelCurrent == last && action == "again") {
        // console.log('againn')
        self.quizPanelCurrent = 0;
        self.quizScore = null;
        self.quizScoreCurrent = null;

        //Run this when the user submits and answer
      } else {
        // console.log('changing panel now')
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
      let next = document.querySelector(".quiz__next");
      let nextClass = "quiz__next--active";

      next.classList.remove(nextClass);
      //Loop through all answers and remove the '--selected' modifier
      answers.forEach((a) => {
        a.classList.remove(targetClass);
      });

      //Add the '--selected' modifier to the selected answer
      target.classList.add(targetClass);
      next.classList.add(nextClass);

      //Check if a score for the current question has been registered.
      //If it's not registered, the just add the score
      if (this.quizScoreCurrent == null) {
        this.quizScoreCurrent += points;

        //If it is registered, clear the score and then add the score
      } else {
        this.quizScoreCurrent = null;
        this.quizScoreCurrent += points;
      }

      // console.log('inside updateScore    ' + document.querySelector(".quiz__question-answer--selected"))
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