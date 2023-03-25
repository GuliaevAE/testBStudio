<template>
  <div class="timerBlock" :class="{active:isOn }">
    <div class="timerBlock_clock">
      <span>{{clock}}</span>
    </div>
    <div class="timerBlock_buttons">
      <img @click="play" v-if="!isOn" :src="PlaySvg" alt />
      <img @click="pause" v-else :src="PauseSvg" alt />
      <img @click="stop" :src="StopSvg" alt />
    </div>
  </div>
</template>

<script>
import PlaySvg from "../assets/images/play.svg";
import PauseSvg from "../assets/images/pause.svg";
import StopSvg from "../assets/images/stop.svg";

export default {
  data() {
    return {
      PlaySvg,
      PauseSvg,
      StopSvg,

      isOn: false,
      timer: null,
      seconds: null,
      minutes: null,
      hours: null
    };
  },
  methods: {
    play() {
      this.isOn = true;
      this.seconds = 0;
      this.timer = setInterval(() => (this.seconds += 1), 1000);
    },
    pause() {
      this.isOn = false;
      clearInterval(this.timer);
    },
    stop() {
      this.isOn = false;
      clearInterval(this.timer);
      this.seconds = 0;
      this.minutes = null;
      this.hours = null;
    }
  },
  computed: {
    clock() {
      if (this.seconds === 60) {
        this.seconds = 0;
        this.minutes !== null ? (this.minutes += 1) : (this.minutes = 1);
      }
      if (this.minutes === 60) {
        this.minutes = 0;
        this.hours ? (this.hours += 1) : (this.hours = 1);
      }

      let hh = this.hours !== null ? this.hours + ":" : "";
      let mm =
        this.minutes !== null
          ? this.minutes >= 10
            ? this.minutes + ":"
            : "0" + this.minutes + ":"
          : "";

      let ss =
        this.seconds !== null
          ? this.seconds >= 10
            ? this.seconds
            : "0" + this.seconds
          : "0";
      return hh + mm + ss;
    }
  }
};
</script>

<style lang="scss">
@font-face {
  font-family: "gothampro";
  src: url(../assets/fonts/GothamPro.ttf);
}
.timerBlock {
  width: 225px;
  height: 120px;
  background: #696969;
  display: flex;
  flex-direction: column;
  color: #9e9e9e;

  .timerBlock_clock {
    height: 50%;
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;

    border-bottom: 1px solid #9e9e9e;

    span {
      font-family: "gothampro";
      font-weight: 400;
      font-size: 22px;
      line-height: 21px;
      text-align: center;
    }
  }
  .timerBlock_buttons {
    display: flex;
    height: 50%;
    width: 100%;
    align-items: center;
    justify-content: space-between;
    padding: 0 70px;
    box-sizing: border-box;

    img {
      height: 20px;
      width: 20px;
      cursor: pointer;
      opacity: 0.5;
    }
  }

  &.active {
    .timerBlock_clock {
      border-bottom: 1px solid white;
      span {
        color: #ffffff;
      }
    }
    img {
      opacity: 1;
    }
  }
}
</style>