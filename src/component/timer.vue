<template>
    <div class="pomodoro__timer">
        <div class="pomodoro__background">
            <div class="timer">{{ formattedTime }}</div>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    props: {
        timeLeft: {
            type: Number,
            required: true,
        },
        mode: {
            type: String,
            required: true,
            default: 'work'
        }
    },
    computed: {
        formattedTime() {
            const minutes = Math.floor(this.timeLeft / 60);
            const seconds = this.timeLeft % 60

            const minutesStr = minutes.toString().padStart(2, '0')
            const secondsStr = seconds.toString().padStart(2, '0')

            return `${minutesStr}:${secondsStr}`
        },
    },
})
</script>

<style scoped>
.pomodoro__background {
    height: 400px;
    width: 400px;
    background-image: url(/src/assets/tomato.png);
    background-repeat: no-repeat;
    background-size: contain;
    position: relative;
    display: flex;
    justify-content: center;
    align-items: center;
}

.timer {
    color: white;
    /* font-weight: bold; */
    font-size: 50px;
}
</style>
