<template>
  <div class="card">
    <section class="time">
      <h1>D-{{ ddays }}</h1>
      <p>{{ dhours }}시간</p>
      <p>{{ dminutes }}분</p>
      <p>{{ dseconds }}초</p>
      <p>{{ percent }} / {{ leftPercent }}%</p>
    </section>
    <hr color="black">
    <section class="config">
      <h2>설정</h2>
      <p class="timeInputForm"><span>시작일: </span><input v-model="startDate"/></p>
      <p class="timeInputForm"><span>종료일: </span><input v-model="endDate"/></p>
    </section>
  </div>
</template>

<script>
import dayjs from 'dayjs';

export default {
  name: 'DDay',
  data() {
    return {
      startDate: '2022-02-07',
      endDate: '2023-08-06',
      currentDay: dayjs(),
      fractionalPartLen: 7,
    }
  },
  mounted() {
    function update() {
      console.log(this.currentDay);
      this.currentDay = dayjs();
    }

    setInterval(update.bind(this), 1);
  },
  computed: {
    ddays() {
      const endDay = dayjs(this.endDate);
      return endDay.diff(this.currentDay, 'days') + 1;
    },
    dhours() {
      const endDay = dayjs(this.endDate);
      return endDay.diff(this.currentDay, 'hours') + 1;
    },
    dminutes() {
      const endDay = dayjs(this.endDate);
      return endDay.diff(this.currentDay, 'minutes') + 1;
    },
    dseconds() {
      const endDay = dayjs(this.endDate);
      return (endDay.diff(this.currentDay, 'microseconds') + 1) / 1000;
    },
    percent() {
      const startDay = dayjs(this.startDate);
      const endDay = dayjs(this.endDate);
      const total = endDay.diff(startDay, 'microseconds');
      const current = this.currentDay.diff(startDay, 'microseconds');
      return Math.round((current / total) * 100 * Math.pow(10, this.fractionalPartLen)) / Math.pow(10, this.fractionalPartLen);
    },
    leftPercent() {
      return Math.round((100 - this.percent) * Math.pow(10, this.fractionalPartLen)) / Math.pow(10, this.fractionalPartLen);
    }
  }
}
</script>

<style scoped>
  .card {
    width: 300px;
    height: 500px;

    background: rgba(255, 255, 255, 0.5);
    border-radius: 20px;

    padding: 20px;
  }

  .time {
    padding: 10px;
  }

  .config {
    padding: 0 10px;
  }

  h1 {
    font-size: 30px;
  }

  h2 {
    font-size: 27px;
  }

  input {
    border: none;
    height: 20px;
    padding: 5px;
    width: 200px;
    background: rgba(255, 255, 255, 0.5);
    border-radius: 5px;
    font-size: 25px;
  }

  section {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .timeInputForm {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  p {
    margin: 0;
    padding: 10px 0;
    font-size: 25px;
  }
</style>
