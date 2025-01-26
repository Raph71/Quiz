<template>
    <div id="quiz">
        <h1>{{ quiz.title }}</h1>
        <Progress :currentStep="currentStep" :totalSteps="quiz.questions.length" />
        <div v-if="end">
            <h2>FIN DU JEU</h2>
            <p>Votre score est de {{ score }} sur {{ quiz.questions.length }}</p>
        </div>
        <Question v-else :question="quiz.questions[currentStep]" :currentStep="currentStep" @changeQuestion="handleQuestion"/>
    </div>
</template>

<script setup>
    import { ref } from 'vue';
    import Progress from './Progress.vue';
    import Question from './Question.vue';

    const currentStep = ref(0);
    const score = ref(0);
    const end = ref(false);

   const props = defineProps({
        quiz: Object
    });

    const handleQuestion = (selectedAnswer) => {

        if (selectedAnswer === props.quiz.questions[currentStep.value].correct_answer) {
            score.value++;
        }

        if (currentStep.value === props.quiz.questions.length - 1) {
            //alert(`Fin du quiz ! Votre score est de ${score.value}/${props.quiz.questions.length}.`);
            finJeu();
        }
        else{
            currentStep.value++;
        }
    }

    const finJeu = () => {
        end.value = true;
    }

</script>

<style>
#quiz{
    margin-left: 10rem;
    margin-right: 10rem;
}
</style>