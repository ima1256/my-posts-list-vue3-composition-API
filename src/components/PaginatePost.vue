<script setup>

defineProps({
    first: Number,
    last: Number,
    numberOfPosts: Number
})

//const emit = defineEmits(['next', 'previous'])

</script>

<template>

    <div class="btn-group" role="group" aria-label="basic-example">
        <button 
            @click="$emit('previous')" 
            :disabled="first == 0" 
            type="button" 
            class="btn btn-outline-primary"
        >
            Previous {{ first }}
        </button>
        <button 
            @click="$emit('next')" 
            :disabled="last >= numberOfPosts" 
            type="button" 
            class="btn btn-outline-primary"
        >
            Next {{ last }}
        </button>
    </div>

</template>

<style>

</style>