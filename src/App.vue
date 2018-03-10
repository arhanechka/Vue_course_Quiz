<template>
  <div id="app">
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1 class="text-center">The Super Quiz</h1>
                 <h2>Total score: {{statistics}}</h2>

            </div>
        </div>
        <hr>
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
    <div v-if="!show && !question">
<app-question-component @answered="answered($event)"></app-question-component></div>
<div v-else-if="!show && question">
<app-wrong-answer-component @onReturnQuestion="wrongQuestion($event)"></app-wrong-answer-component></div>
 <div v-else-if="show && !question"><app-answer-component @onNextQuestion ="nextQuestion($event)" ></app-answer-component> </div> 
 <button @click = "show=!show">status</button>
 </div>
        </div>
    </div>
  </div>
</template>

<script>
import Question from './Question.vue'
import Answer from './Answer.vue'
import WrongAnswer from './WrongAnswer.vue'
export default {
  name: 'app',
  data () {
    return {
      msg: 'Super Quize',
      currentComponent: 'app-question-component',
      show: false,
      question: false,
      statistics: 0
    }
  },
  components:{
    appQuestionComponent: Question,
    appAnswerComponent: Answer,
    appWrongAnswerComponent: WrongAnswer
  },
  methods:{
    answered(answer){
      this.show = answer;
      if(answer == false){
      this.question = true
      this.statistics--;
}
else{this.statistics++}
    },
    nextQuestion(){
      this.show = false;
    },
    wrongQuestion(){
      this.question = false
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
