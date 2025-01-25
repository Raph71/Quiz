<template>
    <div id="question">
        <h2>{{ question.question }}</h2>
        <ul>
            <li v-for="answer in question.choices" :key="answer">
                <input type="radio" :id="answer" :name="`question-${currentStep}`" :value="answer" v-model="selectedAnswer">
                <label :for="answer">{{ answer }}</label>
            </li>
        </ul>
        <button @click="nextQuestion">Question suivante</button>
    </div>
</template>

<script setup>
    import { ref, watch } from 'vue';
    
    const selectedAnswer = ref('');
    

    defineProps({
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
</script>