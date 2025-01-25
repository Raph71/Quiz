<template>
  <div v-if="isLoading">Chargement...</div>
  <div v-else class="container">
    <Quiz :quiz="quiz" v-if="quiz"/>
  </div>
</template>

<script setup>

  // Récupérer les questions dans le fichier JSON
  import { onMounted, ref } from 'vue';
  import Quiz from './composant/Quiz.vue';

  const quiz = ref(null);
  const isLoading = ref(true);

  onMounted(async () => {
    try {
      const response = await fetch('questionaire.json');
      if (!response.ok) throw new Error(`Erreur ${response.status}: ${response.statusText}`);

      const data = await response.json();
      quiz.value = data;
      console.log('Questions récupérées :', quiz.value.questions);
    } catch (error) {
      console.error('Erreur lors de la récupération des questions :', error);
    } finally {
      isLoading.value = false;
    }
  });



</script>

<style>
  .container {
    margin-top: 2rem;
  }
</style>