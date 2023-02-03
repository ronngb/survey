<template>
  <div id="app">
    <form @submit.prevent="submitSurvey()">
      <h1>Survey</h1>
      <h2>Q1: DELIVER THROUGH OTHERS</h2>
      <!-- BUTTONS HERE -->
      <div
        id="Q1"
        class="button-container">
        <button
          type="button"
          class="btn-choice"
          value="A"
          @click="setAnswer($event)">
          A. NOT EFFECTIVE
        </button>
        <button
          type="button"
          class="btn-choice"
          value="B"
          @click="setAnswer($event)">
          B. NEITHER INEFFECTIVE OR EFFECTIVE
        </button>
        <button
          type="button"
          class="btn-choice"
          value="C"
          @click="setAnswer($event)">
          C. EFFECTIVE
        </button>
      </div>

      <h2>Q2: UNDERSTAND OTHERS PERSPECTIVES</h2>
      <!-- BUTTONS HERE -->
      <div
        id="Q2"
        class="button-container">
        <button
          type="button"
          class="btn-choice"
          value="A"
          @click="setAnswer($event)">
          A. NOT EFFECTIVE
        </button>
        <button
          type="button"
          class="btn-choice"
          value="B"
          @click="setAnswer($event)">
          B. NEITHER INEFFECTIVE OR EFFECTIVE
        </button>
        <button
          type="button"
          class="btn-choice"
          value="C"
          @click="setAnswer($event)">
          C. EFFECTIVE
        </button>
      </div>

      <h2>Q3: SOLVE COMPLEX PROBLEMS</h2>
      <!-- BUTTONS HERE -->
      <div
        id="Q3"
        class="button-container">
        <button
          type="button"
          class="btn-choice"
          value="A"
          @click="setAnswer($event)">
          A. NOT EFFECTIVE
        </button>
        <button
          type="button"
          class="btn-choice"
          value="B"
          @click="setAnswer($event)">
          B. NEITHER INEFFECTIVE OR EFFECTIVE
        </button>
        <button
          type="button"
          class="btn-choice"
          value="C"
          @click="setAnswer($event)">
          C. EFFECTIVE
        </button>
      </div>

      <!-- SUBMIT BUTTONS HERE -->
      <button
        class="btn-submit"
        type="submit">
        SUBMIT
      </button>
    </form>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    HelloWorld,
  },
  data() {
    return {
      answersObj: { Q1: '', Q2: '', Q3: '' },
      firebaseURL:
        'https://survey-04-default-rtdb.asia-southeast1.firebasedatabase.app/surveydb/-NNINvYHosA_0Ky19OcL.json',
    }
  },
  mounted() {},
  methods: {
    submitSurvey() {
      if (this.validateAnswer()) {
        window.alert('Please answer all the questions')
      } else {
        window.alert('Thank you for answering all the questions')
        this.storeSurveyData()
          .then((res) => {
            this.clearAnswer()
            this.getSurveyData().then((res) => console.log(res.data))
          })
          .catch((err) => console.log(err))
      }
    },
    setAnswer(e) {
      let btnNodes = e.target.parentNode.childNodes
      btnNodes.forEach((e) => e.classList.remove('active'))
      e.target.classList.add('active')
      this.answersObj[e.target.parentNode.id] = e.target.value
    },
    getSurveyData() {
      return axios.get(this.firebaseURL)
    },
    storeSurveyData() {
      return axios.patch(this.firebaseURL, this.answersObj)
    },
    validateAnswer() {
      for (const prop in this.answersObj) {
        if (this.answersObj[prop] == '') {
          return true
        }
      }
    },
    clearAnswer() {
      let buttons = document.getElementsByClassName('btn-choice')
      for (const button of buttons) {
        button.classList.remove('active')
      }

      for (const prop in this.answersObj) {
        this.answersObj[prop] = ''
      }
    },
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.btn-choice {
  background-color: white;
  margin: 0 10px;
  font-size: 20px;
  padding: 7px;
  border: 1px solid black;
  border-radius: 10px;
}

.btn-choice.active {
  background-color: red;
}

.btn-submit {
  margin-top: 30px;
  background-color: deepskyblue;
  font-size: 20px;
  border: none;
  border-radius: 10px;
  padding: 10px;
}
.btn-submit:active {
  transform: scale(0.8);
  transition: transform 180ms ease-out;
}
</style>
