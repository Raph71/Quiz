<template>
    <div id="quiz">
        <h1>{{ quiz.title }}</h1>
        <p>Votre score : {{ score }}</p>
        <Progress :currentStep="currentStep" :totalSteps="quiz.questions.length" />
        <Question :question="quiz.questions[currentStep - 1]" :currentStep="currentStep" @changeQuestion="handleQuestion"/>
    </div>
</template>

<script setup>
    import { ref } from 'vue';
    import Progress from './Progress.vue';
    import Question from './Question.vue';

    const currentStep = ref(1);
    const score = ref(0);

   const props = defineProps({
        quiz: Object
    });

    const handleQuestion = (selectedAnswer) => {

        if (selectedAnswer === props.quiz.questions[currentStep.value - 1].correct_answer) {
            score.value++;
        }

        if (currentStep.value === props.quiz.questions.length) {
            alert(`Fin du quiz ! Votre score est de ${score.value}/${props.quiz.questions.length}.`);
            currentStep.value = 1;
            score.value = 0;
        }
        else{
            currentStep.value++;
        }
    }

</script>