<template>
    <label :for="id" :class="classes">
        <input :disabled="disabled" type="radio" :id="id" name="answer" :value="value" v-model="model"/>
        {{ value }}
    </label>
</template>

<script setup>
    import { computed } from 'vue';

    const props = defineProps({
        id: String,
        disabled: Boolean,
        value: String,
        correctAnswer: String,
    })

    const model = defineModel();
    const classes = computed(() => {
        return {
            'disabled': props.disabled,
            'correct': props.disabled && props.value === props.correctAnswer,
            'incorrect': props.disabled && props.value !== props.correctAnswer && props.value === model.value,
        }
    })
</script>

<style>
.correct {
    color: green;
    opacity: 1 !important;
}
.incorrect {
    color: red;
    opacity: 1 !important;
}
.disabled {
    opacity: 0.5;
}
</style>