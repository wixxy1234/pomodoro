<style scoped></style>

<template>
  <div class="pomodoroTimer">
    <Timer :timeLeft="timeLeft" :mode="mode"></Timer>
    <div class="btns_wrapper">
      <Button @click="startTimer" :isRunning="isRunning">Старт</Button>
      <Button @click="stopTimer" :isRunning="!isRunning">Стоп</Button>
      <Button @click="resetTimer">Заново</Button>
    </div>
  </div>
</template>


<script lang="ts">
import { defineComponent } from 'vue';
import Timer from './component/timer.vue';
import Button from './component/button.vue';


export default defineComponent({
  components: { Timer, Button },
  data() {
    return {
      // timer: 0,
      mode: 'break' as 'break' | 'work',
      isRunning: false,
      timeLeft: 0.3 * 60, // 25мин
      workTime: 25 * 60,
      breakTime: 5 * 60,
      timerId: null as number | null,
    }
  },
  methods: {
    startTimer() {
      if (this.isRunning) return

      this.isRunning = true

      this.timerId = setInterval(() => {
        if (this.timeLeft > 0) {
          this.timeLeft -= 1
        } else {
          this.switchMode()
        }
      }, 1000)
    },
    stopTimer() {
      if (this.timerId) {
        clearInterval(this.timerId)
        this.timerId = null
      }
      this.isRunning = false
    },
    resetTimer() {
      this.stopTimer()
      this.mode = 'work'
      this.timeLeft = this.workTime
    },
    switchMode() {
      this.stopTimer()

      if (this.mode = 'work') {
        this.mode = 'break'
        this.timeLeft = this.breakTime
        setTimeout(this.startTimer, 5000)

      } else {
        this.mode = 'work'
        this.timeLeft = this.workTime
        setTimeout(this.startTimer, 5000)

      }
    },
  }
})
</script>

<style scoped>
.pomodoroTimer {
  margin: 0 auto;
  margin-top: 100px;
  width: 400px;
}

.btns_wrapper {
  display: flex;
  justify-content: space-between;
}
</style>