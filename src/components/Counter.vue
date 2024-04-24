<template>
  <div>
    <h2>Countdown Timer</h2>
    <div class="root-counter">
      <section
        class="wrap-counter"
        v-for="counterTime in counterTimer"
        :key="counterTime.timeName"
      >
        <div class="counter">
          {{ counterTime.value }}
          <span class="counter-text">{{ counterTime.timeName }}</span>
        </div>
        <span v-if="counterTime.devider">:</span>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: "CounterComponent",
  data() {
    return {
      counterTimer: [
        {
          timeName: "days",
          value: 0,
          devider: true,
        },
        {
          value: 0,
          timeName: "hours",
          devider: true,
        },
        {
          value: 0,
          timeName: "minutes",
          devider: true,
        },
        {
          value: 0,
          timeName: "seconds",
          devider: false,
        },
      ],
    };
  },
  computed: {
    _seconds: () => 1000,
    _minutes() {
      return this._seconds * 60;
    },
    _hours() {
      return this._minutes * 60;
    },
    _days() {
      return this._hours * 24;
    },
  },
  methods: {
    getCounter() {
      const timer = setInterval(() => {
        const startDate = new Date();
        const endDate = new Date(2022, 5, 15, 8, 44, 10, 10);
        const distance = endDate.getTime() - startDate.getTime();

        const days = Math.floor(distance / this._days);
        const hours = Math.floor((distance % this._days) / this._hours);
        const minutes = Math.floor((distance % this._hours) / this._minutes);
        const seconds = Math.floor((distance % this._minutes) / this._seconds);

        this.counterTimer[0].value = days < 10 ? "0" + days : days;
        this.counterTimer[1].value = hours < 10 ? "0" + hours : hours;
        this.counterTimer[2].value = minutes < 10 ? "0" + minutes : minutes;
        this.counterTimer[3].value = seconds < 10 ? "0" + seconds : seconds;

        if (distance < 0) {
          clearInterval(timer);
          this.counterTimer[0].value = 0;
          this.counterTimer[1].value = 0;
          this.counterTimer[2].value = 0;
          this.counterTimer[3].value = 0;
          return false;
        }
      }, 1000);
    },
  },
  created() {
    this.getCounter();
  },
};
</script>

<style scoped>
.root-counter {
  display: flex;
  justify-content: center;
}
.wrap-counter {
  display: flex;
  justify-content: center;
  justify-items: center;
  font-size: 6rem;
}
.wrap-counter > span:last-child {
  padding-left: 18px;
  padding-right: 18px;
}
.counter {
  position: relative;
}
.counter-text {
  position: absolute;
  font-size: 1rem;
  bottom: -4px;
  left: 0;
  right: 0;
  margin-left: auto;
  margin-right: auto;
}
/* nelson setyawan - Vue Countdown Timer */
</style>
