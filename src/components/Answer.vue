<template>

    <label :for="id" :class="classes" >
        <input :disabled="disabled" 
        :value="value" type="radio" 
        name="answer" :id="id" 
        v-model="model"
        @change="onChange">{{ value }}
    </label>
</template>

<script setup>
import { computed } from 'vue';


    const props = defineProps({
        id : String,
        disabled : Boolean,
        value : String,
        correctAnswer : String
    })
    const model = defineModel()
    const emits = defineEmits(['change'])
    
    const onChange = (event) => {
        emits('change', event)
    }

    const classes = computed(() => ({
        disabled : props.disabled,
        right : props.disabled && 
        props.value === props.correctAnswer,
        wrong : props.disabled && 
        props.value !== props.correctAnswer && 
        model.value === props.value
    }))

</script>

<style>

.disabled {
    opacity: .5;
}

.right{
    opacity: 1;
    color: rgb(0, 255, 0);
}

.wrong{
    opacity: 1;
    color: red;
}
</style>