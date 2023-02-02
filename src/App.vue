<template>
  <div id="app">
    <form @submit.prevent="">
      <h1>Survey</h1>
      <h2>Q1: DELIVER THROUGH OTHERS</h2>
      <!-- BUTTONS HERE -->
      <div class="button-container">
        <button
          class="btn-choice"
          @click="setAnswer('Q1', 'A')">
          A. NOT EFFECTIVE
        </button>
        <button
          class="btn-choice"
          @click="setAnswer('Q1', 'B')">
          B. NEITHER INEFFECTIVE OR EFFECTIVE
        </button>
        <button
          class="btn-choice"
          @click="setAnswer('Q1', 'C')">
          C. EFFECTIVE
        </button>
      </div>

      <h2>Q2: UNDERSTAND OTHERS PERSPECTIVES</h2>
      <!-- BUTTONS HERE -->
      <h2>Q3: SOLVE COMPLEX PROBLEMS</h2>
      <!-- BUTTONS HERE -->

      <!-- SUBMIT BUTTONS HERE -->
      <button
        type="submit"
        @click="testFn()">
        SUBMIT
      </button>
    </form>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
  },
  data() {
    return {
      answersObj: { Q1: '', Q2: '', Q3: '' },
    }
  },
  mounted() {
    // console.log(this.answersObj.Q1)
  },
  updated() {
    console.log(this.answersObj)
  },
  methods: {
    setAnswer(prop, answer) {
      this.answersObj[prop] = answer
      console.log(this.answersObj)
    },
    testFn() {
      console.log('HelloWorld')
    },
    testFn1() {
      console.log(1)
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

.button-container > button {
  margin: 0 10px;
  font-size: 20px;
  background-color: white;
  padding: 7px;
  border: 1px solid black;
  border-radius: 10px;
}

.btn-choice: ;
</style>
