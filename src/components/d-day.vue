<template>
  <div class="hello">
    D-{{ days }}
  </div>
</template>

<script>
import dayjs from 'dayjs';

export default {
  name: 'DDay',
  data() {
    return {
      days: 0
    }
  },
  mounted() {
    const date1 = dayjs('2023-08-06');
    const date2 = dayjs();
    const dDays = date1.diff(date2, 'days') + 1;
    this.days = dDays;
  }
}
</script>

<style scoped>
</style>
