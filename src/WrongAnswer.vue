<template>
    <div class="alert alert-danger text-center">
        <h1>That's Incorrect! Try again!</h1>
        <hr>
        <button class="btn btn-primary" @click="onReturnQuestion">Next Question</button>
    </div>
</template>



<script>
export default {
 
  data () {
    return {
      msg: 'Answer'
    }
  },
  methods:{
    onReturnQuestion(){
      this.$emit('onReturnQuestion')
    }
  }
}
</script>