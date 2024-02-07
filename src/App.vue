<template>
 <div class="ctr">
    <transition name="fade" mode="out-in">

        <Questions v-if="questionsAnswerd < questions.length"
        :questions="questions"
        :questionsAnswerd="questionsAnswerd"
        :isAnswered="isAnswered"
        @question-answered="questionAnswerd"
        />
        
        <Results v-else 
        :results="results"
        :totalCorrect="totalCorrect" />
    </transition>
    
        <h4 class="question">You have <span>{{ totalCorrect }}</span> correct answers</h4>   

        <button type="button" 
        class="reset-btn" 
        @click="reset"
        v-if="questionsAnswerd === questions.length">
        >Reset</button>
</div>

</template>

<script >
import Questions from './components/Questions.vue'
import Results from './components/Results.vue'
export default {
  name: "App",
  components: {
    Questions,
    Results
  },
  data() {
    return {
      questionsAnswerd:0,
      totalCorrect:0,
      isAnswered:false,
      questions: [
          {
              q: 'What is 2 + 2?', 
              answers: [
                  {
                      text: '4',
                      is_correct: true
                  },
                  {
                      text: '3',
                      is_correct: false 
                  },
                  {
                      text: 'Fish',
                      is_correct: false 
                  },
                  {
                      text: '9',
                      is_correct: false 
                  }
              ] 
          },
          { 
              q: 'How many letters are in the word "Banana"?', 
              answers: [
                  {
                      text: '5',
                      is_correct: false
                  },
                  {
                      text: '7',
                      is_correct: false 
                  },
                  {
                      text: '6',
                      is_correct: true 
                  },
                  {
                      text: '12',
                      is_correct: false 
                  }
              ] 
          },
          { 
              q: 'Find the missing letter: C_ke', 
              answers: [
                  {
                      text: 'e',
                      is_correct: false
                  },
                  {
                      text: 'a',
                      is_correct: true 
                  },
                  {
                      text: 'i',
                      is_correct: false 
                  }
              ] 
          },
      ],
      results: [
          {
              min: 0,
              max: 2,
              title: "Try again!",
              desc: "Do a little more studying and you may succeed!"
          },
          {
              min: 3,
              max: 3,
              title: "Wow, you're a genius!",
              desc: "Studying has definitely paid off for you!"
          }
      ]
    }
  },
  methods: {
    questionAnswerd(is_correct) {
      if(is_correct) {
        this.totalCorrect++;
        console.log(this.totalCorrect);
      }
      this.isAnswered = true;
      setTimeout(() => {
          this.questionsAnswerd++;
          this.isAnswered = false;
      }, 1000);

    },
    reset() {
      this.questionsAnswerd = 0;
      this.totalCorrect = 0;
    }
  }
}

</script>


