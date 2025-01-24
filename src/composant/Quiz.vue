<template>
    <div id="quiz">
        <h1>{{ quiz.title }}</h1>
    </div>
</template>

<script setup>
    import { ref } from 'vue';

    defineProps({
        quiz: Object
    })

</script>