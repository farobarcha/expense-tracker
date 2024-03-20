<template>
    <h4>Your Balance</h4>
    <h1 id="balance">${{ totalBalance }}</h1>
</template>

<script setup>
defineProps({
    totalBalance: {
        type: Number,
        default: 0,
    }
})
</script>