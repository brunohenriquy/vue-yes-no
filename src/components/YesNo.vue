<template>
  <div id="watch-example">
    <p>
      Ask a yes/no question:
      <input v-model="question">
    </p>
    <p>{{ answer }}</p>
    <p><img v-bind:src="image"></p>
  </div>
</template>

<script>
  import {debounce, capitalize} from 'lodash'
  import axios from 'axios'

  export default {
    name: 'HelloWorld',
    data() {
      return {
        question: '',
        answer: 'I cannot give you an answer until you ask a question!',
        image: ''
      }
    },
    watch: {
      // whenever question changes, this function will run
      question: function (newQuestion, oldQuestion) {
        console.log(oldQuestion)
        console.log(newQuestion)
        this.image = ''
        this.answer = 'Waiting for you to stop typing...'
        this.debouncedGetAnswer()
      }
    },
    created: function () {
      this.debouncedGetAnswer = debounce(this.getAnswer, 500)
    },
    methods: {
      getAnswer: function () {
        if (this.question.indexOf('?') === -1) {
          this.image = ''
          this.answer = 'Questions usually contain a question mark. ;-)'
          return
        }
        this.answer = 'Thinking...'
        var vm = this
        axios.get('https://yesno.wtf/api')
          .then(function (response) {
            vm.image = capitalize(response.data.image)
            vm.answer = capitalize(response.data.answer)
          })
          .catch(function (error) {
            vm.answer = 'Error! Could not reach the API. ' + error
          })
      }
    }
  }
</script>
