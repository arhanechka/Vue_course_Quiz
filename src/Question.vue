<template>
    <div class="panel panel-default">
        <div class="panel-heading">
            <h3 class="panel-title text-center">{{ taskPhrase }}</h3>
        </div>
        <div class="panel-body" v-for="answer in answers">
            <div class="col-xs-12 col-sm-6 text-center"> {{answer}} <br>
                <button class="btn btn-primary btn-lg" style="margin: 10px" @click = "checkAnswer(answer)">{{ msg }}</button>
            </div>
         </div>
    </div>
</template>

<script>
  const MODE_ADDITION = 1;
    const MODE_SUBTRACTION = 2;

export default {
 
  data () {
    return {
      msg: "Answer",
      firstNumber: 0,
      secondNumber: 0,
      mode: 0,
      operation: '',
      taskPhrase: '',
      answer: {
          number: 0,
          correct: false
      },
      answers: [],
      rightAnswer: 0
    }
  },
 created(){
  this.firstNumber = this.generateRandomNumber(1,100) 
  this.secondNumber = this.generateRandomNumber(1,100)
  this.mode = this.generateRandomNumber(1,2)
  this.createTask();
  this.generateAnswer();
 },
  methods:{
      createTask(){
          if (this.mode == 1){
              this.operation = '+'
              this.rightAnswer = this.firstNumber + this.secondNumber;
              this.taskPhrase = "What's " + this.firstNumber + this.operation + this.secondNumber +'?';
          }
          else {this.operation = '-'
          if (this.firstNumber>this.secondNumber){
              this.taskPhrase = "What's " + this.firstNumber + this.operation + this.secondNumber+'?';
              this.rightAnswer = this.firstNumber - this.secondNumber;
          }
          else{
              this.taskPhrase = "What's " + this.secondNumber + this.operation + this.firstNumber+'?';
              this.rightAnswer = this.secondNumber - this.firstNumber;
          }}
          console.log(this.rightAnswer)
      },
      generateRandomNumber(min, max){
          return Math.round(Math.random() * (max - min)) + min;
      },
      generateAnswer(){
          var place = this.generateRandomNumber(0,3)
          for (var i =0; i<4; i++){
              this.answers[i]= this.generateRandomNumber(0, 200)
          }
          this.answers[place] = this.rightAnswer
          console.log(this.answers)
      },
      checkAnswer(answer){
          if (answer == this.rightAnswer){
        //       alert ("Right!")
        //       location.reload(true)
          this.$emit('answered', true) 
          }
        //   else alert ("Bad!")
        //   this.createTask();
        
       else{ 
          this.$emit('answered', false)
      }}
  }
}
</script>