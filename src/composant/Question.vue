<template>
    <div id="question">
        <h2>{{ question.question }}</h2>
        <ul>
            <li v-for="(answer, index) in randomChoices" :key="answer">
                <Choix :id="`choix${index}`" :disabled="hasanswered" :value="answer" :correctAnswer="question.correct_answer" v-model="selectedAnswer"/>
            </li>
        </ul>
        <button @click="nextQuestion">Question suivante</button>
    </div>
</template>

<script setup>
    import { computed, ref, watch } from 'vue';
    import Choix from './Choix.vue';
import { shuffleArray } from '@/array';
    
    const selectedAnswer = ref('');
    const hasanswered = computed(() => selectedAnswer.value !== '');

    
    const props = defineProps({
        question: Object,
        currentStep: Number
    })

    const emit = defineEmits(['changeQuestion']);

    const nextQuestion = () => {
        if (!selectedAnswer.value) {
            alert('Veuillez sélectionner une réponse avant de continuer.');
        }
        else {
            emit('changeQuestion', selectedAnswer.value);
            selectedAnswer.value = '';
        }
    }
    // Shuffle the choices
    const randomChoices = computed(() => shuffleArray(props.question.choices));
</script>

<style>
#question {
    margin-top: 2rem;
}
#question button{
    margin-left: auto;
    display: block;
}
</style>