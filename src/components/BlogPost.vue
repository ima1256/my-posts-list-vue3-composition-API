<script setup>

//defineProps(['title', "content", "id", "colorText"])

defineProps({
    title: String,
    content: {
        type: String,
        default: "Without content"
    },
    id: Number
})

//const emit = defineEmits(['changeFavorites'])

</script>

<template>

<div class="card">
    <div class="card-body" >
        <h5 class="card-title"> {{ id }} - {{ title }}</h5>
        <p>{{ content }}</p>
        <button @click="$emit('changeFavorite', title)" class="btn btn-outline-primary"> Favorite </button>
    </div>
</div>

</template>

<style>

</style>