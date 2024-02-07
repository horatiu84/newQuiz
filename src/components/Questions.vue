<template>
    <div class="questions-ctr">
        <div class="progress">
            <div class="bar" :style="{ width : `${(questionsAnswerd / questions.length) * 100}%`}"></div>
            <div class="status">{{ questionsAnswerd }} out of {{ questions.length }} questions answered</div>
        </div>
        <TransitionGroup name="fade"> 
            <div class="single-question" 
                v-for="(question,qi) in questions"
                :key="question.q"
                v-show="questionsAnswerd === qi">
                <div class="question">{{ question.q }}</div>
                <div class="answers"  >
                    <div class="answer"
                    :class="[{'rightAnswer': answer.is_correct&&isAnswered }, {'wrongAnswer': !answer.is_correct&&isAnswered}]"    
                    v-for="answer in  question.answers"
                    :key="answer.text"
                    @click.prevent="selectAnswer(answer.is_correct)"
                    >
                    {{answer.text }}
                    </div>
                
                </div>
            </div>
        </TransitionGroup>
    </div>
</template>

<script>
    export default {
        props: ['questions','questionsAnswerd','isAnswered'],
        emits: ['question-answered'],
        methods: {
            selectAnswer(is_correct) {
                this.$emit('question-answered', is_correct)
            },
        },
    }
</script>