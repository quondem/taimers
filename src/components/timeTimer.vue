<template lang="">
  <div class="timer">
    <span class="timer__time" :class="{ active }">{{ fullTime }}</span>
    <div class="hr" :class="{ active }"></div>
    <div class="buttons">
      <transition name="fade" mode="out-in">
        <div v-if="!active" @click="play" :class="{ active }">
          <svg
            width="17"
            height="20"
            viewBox="0 0 17 20"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path class="icon" d="M0 20V0L17 10L0 20Z" fill="#9E9E9E" />
          </svg>
        </div>
        <div v-else @click="play" :class="{ active }">
          <svg
            width="10"
            height="20"
            viewBox="0 0 10 20"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <rect x="7" width="3" height="20" fill="#9E9E9E" />
            <rect width="3" height="20" fill="#9E9E9E" />
          </svg>
        </div>
      </transition>
      <div @click="stop" :class="{ active }" class="stop">
        <svg
          width="20"
          height="20"
          viewBox="0 0 20 20"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <rect width="20" height="20" fill="#9E9E9E" />
        </svg>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      time: 0,
      active: false,
      started: false,
    };
  },
  methods: {
    play() {
      this.active = !this.active;
      if (this.active && !this.started) {
        this.started = true;
        let timer = setInterval(() => {
          if (this.active) {
            this.time++;
          } else {
            clearInterval(timer);
            this.started = false;
          }
        }, 1000);
      }
    },
    stop() {
      this.started = false;
      this.active = false;
      this.time = 0;
    },
  },
  computed: {
    fullTime() {
      let hours = Math.floor(this.time / 60 / 60);
      let minutes = Math.floor(this.time / 60) - hours * 60;
      let seconds = this.time % 60;
      if (hours) {
        return hours + ":" + minutes + ":" + seconds;
      } else if (minutes) {
        return minutes + ":" + seconds;
      } else {
        return seconds;
      }
    },
  },
};
</script>
<style>
.buttons div {
  cursor: pointer;
  max-height: 20px;
  transition: all 0.3s;
}
.timer {
  transition: all 0.5s;
  max-width: 100%;
  height: 120px;
  background-color: #696969;
  box-sizing: border-box;
  padding-top: 22px;
  text-align: center;
}
.timer__time {
  font-family: "Gotham Pro", sans-serif;
  font-style: normal;
  font-weight: 400;
  font-size: 22px;
  line-height: 21px;
  color: #9e9e9e;
  transition: all 0.3s;
}
.hr {
  width: 100%;
  height: 1px;
  margin-top: 20px;
  background-color: #9e9e9e;
  transition: all 0.3s;
}
.buttons {
  width: 85px;
  display: flex;
  justify-content: space-between;
  margin: 20px auto 0 auto;
}
span.timer__time.active {
  color: #ffffff;
}
div.hr.active {
  background-color: #ffffff;
}
.active svg path {
  fill: #ffffff;
}
.active svg rect {
  fill: #ffffff;
}
svg path {
  transition: all 0.3s;
}
svg rect {
  transition: all 0.3s;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.25s;
  transform: scale(0.9);
}
.stop:active {
  transition: scale 0.2s;
  transform: scale(0.9);
}
</style>
