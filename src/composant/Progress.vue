<template>
    <div>Etape {{ currentStep + 1 }} sur {{ totalSteps }}</div>
    <progress :value="currentStep" :max="totalSteps-1"/>
</template>

<script setup>

    defineProps({
        currentStep: Number,
        totalSteps: Number
    })  

</script>