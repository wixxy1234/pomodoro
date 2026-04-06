<template>
    <button type="button" :disabled="isRunning">
        <slot></slot>
    </button>
</template>

<script lang="ts">
export default {
    props: {
        isRunning: {
            type: Boolean,
            default: false
        }
    }
}
</script>

<style scoped>
button {
    border-radius: 10px;
    padding: 10px 20px;
    background-color: #569c14;
    color: white;
    border: none;
    font-weight: bold;
    cursor: pointer;
    margin: 10px 20px;
}

button:hover {
    background-color: #569c14d7;
}

button:disabled {
    opacity: 0.5;
    cursor: not-allowed;
}
</style>