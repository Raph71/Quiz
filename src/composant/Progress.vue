<template>
    <div>Etape {{ currentStep }} sur {{ totalSteps }}</div>
</template>

<script setup>
    import { ref } from 'vue';

    defineProps({
        currentStep: Number,
        totalSteps: Number
    })  

</script>