<template>
  <div class="container">
   
    <div class="block__time" v-for="(timer, index) in timers" :key="index" :class="{active: timer.isActive}" >
      <div class="block__timer">
          <p class="timer">{{ formatTime(timer.time) }}</p>
      </div>
      <div class="block__settings">
            <button @click="toggleTimer(timer,index)"><img :src="timer.iconSrc" alt="play" class="play"></button>
            <button @click="resetTimer(timer)"><img :src="timer.iconStop" alt="" class="stop"></button> 
      </div>

    </div>
    <div class="add__timer">
      <button @click="addTimer()"><img src="@/assets/img/plus.png" alt=""></button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Stopwatch',
  props: {
    msg: String
  },
  data() {
    return {
      timers: [],
    };
  },
  methods: {
    addTimer() {
      console.log('addTime')
      const newTimer = {
        time: 0,
        intervalId: null,
        isActive: false,
        iconSrc: require('@/assets/img/play.png'),
        iconStop: require('@/assets/img/stop.png')    
      };
      this.timers.push(newTimer);
    },
    startTimer(timer) {
      timer.intervalId = setInterval(() => {
        timer.time++;
      }, 1000);
      timer.isActive = true;
    },
    pauseTimer(timer) { 
      clearInterval(timer.intervalId);
      timer.isActive = false;
    },
    resetTimer(timer) {
      console.log(timer)
      clearInterval(timer.intervalId);
      timer.time = 0;
      timer.isActive = false;
      timer.intervalId = null,
      timer.iconSrc = require('@/assets/img/play.png');
    },
    toggleTimer(timer,index) {
      console.log(timer.isActive)
      if (!timer.isActive) {
        this.startTimer(timer);
        timer.iconSrc = require('@/assets/img/pause.png');
      } else {
        this.pauseTimer(timer);
        timer.iconSrc = require('@/assets/img/play.png');
      }
    },
    formatTime(time) {
      const hours = Math.floor(time / 3600);
      const minutes = Math.floor((time % 3600) / 60);
      const seconds = time % 60;

      if (hours > 0) {
        return `${hours.toString()}:${minutes.toString()}:${seconds.toString()}`;
      } else if (minutes > 0) {
        return `${minutes.toString()}:${seconds.toString()}`;
      } else {
        return `${seconds.toString()}`;
      }
    }
  },
};
</script>

<style scoped>

  .container {
    max-width: 775px;
    height: fit-content;
    display: flex;
    position: relative;
    justify-content: center;
    flex-wrap: wrap;
    gap: 50px;
  }
  .block__time {
        display: flex;
        position: relative;
        flex-direction: column;
        width: 225px;
        height: 120px;
        background: #696969; 
    }

    .add__timer {
        display: flex;
        justify-content: center;
        align-items: center;
        position: relative;
        width: 225px;
        height: 120px;
        background: #696969;
    }

    .add__timer button {
      color: #9E9E9E;
    }

    .block__timer {
       display: flex;
        position: relative;
        background: transparent;
        height: 60px;
        border-bottom: 1px solid #9E9E9E;
        justify-content: center;
        align-items: center;
    }


    .timer {
        display: inline;
        font-weight: 400;
        font-size: 22px;
        line-height: 21px;
        text-align: center;
        color: #9E9E9E;
    }
    .block__settings {
        display: flex;
        position: relative;
        align-items: center;
        justify-content: center;
        height: 60px;
        gap: 48px;  
    }

    button {
        background: transparent;
        outline: none;
        border: none;
        padding: 0;
        margin: 0;
        cursor: pointer;
    }
    .active .block__timer {
      border-bottom: 1px solid #fff;
    }
    .active .block__timer .timer{
      color: #fff;
    }
    .active img {
      filter: brightness(0) invert(1);
    }

</style>