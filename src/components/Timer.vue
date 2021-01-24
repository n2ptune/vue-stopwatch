<template>
  <div class="timer-wrapper">
    <div class="time-table">
      <div class="time minutes">{{ minutesWithString }}</div>
      <div class="separate">:</div>
      <div class="time seconds">{{ secondsWithString }}</div>
    </div>
    <Events @start="start" @reset="reset" @stop="stop" />
  </div>
</template>

<script>
import { ref, computed } from 'vue';
import Events from './Events.vue';

export default {
  components: {
    Events
  },

  setup() {
    const seconds = ref(0);
    const minutes = ref(0);
    const running = ref(false);
    const timer = ref(null);

    const transform = value => {
      return value > 9 ? value.toString() : '0' + value;
    };

    const secondsWithString = computed(() => transform(seconds.value));
    const minutesWithString = computed(() => transform(minutes.value));

    const startTimer = () => {
      return setInterval(() => {
        if (seconds.value >= 59) {
          seconds.value = 0;
          minutes.value += 1;
        } else {
          seconds.value += 1;
        }
      }, 1000);
    };

    // events
    const start = () => {
      if (running.value) {
        return;
      }

      running.value = true;
      timer.value = startTimer();
    };

    const stop = () => {
      if (!running.value || !timer.value) {
        return;
      }

      clearInterval(timer.value);
      running.value = false;
    };

    const reset = () => {
      running.value = false;

      if (timer.value) {
        clearInterval(timer.value);
      }

      timer.value = null;
      seconds.value = 0;
      minutes.value = 0;
    };

    return {
      secondsWithString,
      minutesWithString,
      start,
      stop,
      reset
    };
  }
};
</script>

.<style scoped>
.time-table > * {
  display: inline-block;
  margin: 0 5px;
}
.time-table .separate {
  margin: 0 1px;
}
.time-table .time {
  font-size: 1.5rem;
}
</style>
