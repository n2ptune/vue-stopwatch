<template>
  <div class="events">
    <button @click="$emit('start')">시작</button>
    <button @click="$emit('stop')">중지</button>
    <button @click="$emit('reset')">리셋</button>
  </div>
</template>

<script>
export default {
  emits: ['start', 'stop', 'reset']
};
</script>

<style scoped>
.events button {
  margin-right: 5px;
}
</style>
