<template>
  <div class="questionsContainer" v-if="questions[counter] && !this.displayResult">
    <h3 class="question">{{ questions[counter].question}}</h3>
    <div class="answers" id="answers" v-for="(answer, index) in questions[counter].answers" :key="answer.id">
      <button
        :class="answer.selected ? 'answer active' : 'answer'"
        type="button"
        name="quizAnswers"
        @click="selectAnswer(answer, index)"
      >
        {{ answer.name }}
      </button>
    </div>
    <button
      type="button"
      id="next"
      @click="next"
      value="chosenAnswer"
      v-if="counter < questions.length - 1"
    >
      Next
    </button>
    <button
      type="button"
      id="submit"
      @click="submit"
      v-if="counter === questions.length - 1"
    >
      Submit
    </button>
  </div>
  <p class="result" v-if="this.displayResult">{{this.name}}, you scored {{this.numberOfCorrects}} out of 5!</p>
</template>

<script>
  import Swal from "sweetalert2";
  export default {
    name: 'Questions',
    props: ['name'],
    data() {
      return {
        counter: 0,
        questions: [
          {
            id: 1,
            question: "Q1. What is one thing that will always cheer me up?",
            answers: [
              {
                id: "coffee",
                name: "Coffee",
                correct: true,
                selected: false
              },
              {
                id: "chocolate",
                name: "Chocolate",
                correct: false,
                selected: false
              },
              {
                id: "cake",
                name: "Cake",
                correct: false,
                selected: false
              },
              {
                id: "books",
                name: "Books",
                correct: false,
                selected: false
              }
            ],
          },
          {
            id: 2,
            question: "Q2. Which of the following places I would choose?",
            answers: [
              {
                id: "gloria",
                name: "Gloria Jeans",
                correct: false,
                selected: false
              },
              {
                id: "second",
                name: "Second Cup",
                correct: false,
                selected: false
              },
              {
                id: "starbucks",
                name: "Starbucks",
                correct: true,
                selected: false
              },
              {
                id: "cinnabon",
                name: "Cinnabon",
                correct: false,
                selected: false
              }
            ],
          },
          {
            id: 3,
            question: "Q3. Which of the following cities I would visit again and again?",
            answers: [
              {
                id: "rome",
                name: "Rome",
                correct: false,
                selected: false
              },
              {
                id: "paris",
                name: "Paris",
                correct: false,
                selected: false
              },
              {
                id: "berlin",
                name: "Berlin",
                correct: false,
                selected: false
              },
              {
                id: "dubai",
                name: "Dubai",
                correct: true,
                selected: false
              }
            ],
          },
          {
            id: 4,
            question: "Q4. What is my favorite food?",
            answers: [
              {
                id: "burger",
                name: "Burger",
                correct: true,
                selected: false
              },
              {
                id: "pizza",
                name: "Pizza",
                correct: false,
                selected: false
              },
              {
                id: "sushi",
                name: "Sushi",
                correct: false,
                selected: false
              },
              {
                id: "pasta",
                name: "Pasta",
                correct: false,
                selected: false
              }
            ],
          },
          {
            id: 5,
            question: "Q5. Favorite time of the week?",
            answers: [
              {
                id: "fridayEvening",
                name: "Friday evening",
                correct: true,
                selected: false
              },
              {
                id: "saturdayEvening",
                name: "Saturday evening",
                correct: false,
                selected: false
              },
              {
                id: "saturdayMorning",
                name: "Saturday morning",
                correct: false,
                selected: false
              },
              {
                id: "sundayMorning",
                name: "Sunday morning",
                correct: false,
                selected: false
              }
            ],
          }
        ],
        numberOfCorrects: 0,
        displayResult: false
      }
    },
    methods: {
      next() {
        if(!this.questions[this.counter].answers.some(answer => answer.selected === true)) {
          Swal.fire("Error", "You haven't selected anything", "error")
        }
        this.counter++;
      },
      selectAnswer(currentAnswer, index) {
        this.questions[this.counter].answers = this.questions[this.counter].answers.map(answer => ({...answer, selected: false}))
        this.questions[this.counter].answers[index].selected = true

        if(currentAnswer.correct) {
          this.numberOfCorrects++;
        }
      },
      submit() {
        this.displayResult = true;
      }
    }
  }
</script>

<style lang="scss" scoped>
  .questionsContainer {
    display: flex;
    flex-wrap: wrap;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100vh;
    border-radius: 10px;
    padding: 25px 5px;
  }

  .question {
    color: #F9F6EE;
  }

  .answer {
    display: inline-block;
    background-color: #F9F6EE;
    text-align: center;
    padding: 10px;
    margin: 7px;
    width: 200px;
    border-radius: 4px;
    border: transparent;
    cursor: pointer;
    transition: 0.1s;

    &.active {
      background-color: #686de0;
      color: #F9F6EE;
    }

    &:hover {
      background-color: #ddd;
    }
  }

  #next {
    border: transparent;
    border-radius: 5px;
    background-color: #686de0;
    color: #fff;
    padding: 6px 12px;
    font-size: 15px;
    cursor: pointer;
    margin: 10px 0;
  }

  #submit {
    border: transparent;
    border-radius: 5px;
    background-color: #41B883;
    color: #fff;
    padding: 6px 12px;
    font-size: 15px;
    cursor: pointer;
    margin: 10px 0;
  }

  .result {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    height: 100vh;
    align-items: center;
    color: #F9F6EE;
    font-style: italic;
    font-size: 42px;
  }
</style>
