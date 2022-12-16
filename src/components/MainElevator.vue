<template>
    <div class="shaft">
        <li v-for="floor in floors" :key="floor" class="floor">{{floor}}</li>
        <div
          :style="{'bottom': `${(current - 1)* 216}px`,
          'transition-duration': `${time.toString()[0]}s`}"
          :class="{'elevator elevator-animation': isDoors, 'elevator': !isDoors}"
        >
        <div class="floor__panel">
          <div class="floor__icon floor__up" v-if="prev < current && isRun"></div>
          <div class="floor__icon floor__down" v-else-if="isRun"></div>
          <div class="current-floor">{{current}}</div>
        </div>
        </div>
    </div>
</template>

<script>
export default {
  data() {
    return {
      prev: +localStorage.getItem('prev') || 0,
      time: +localStorage.getItem('time') || 3000,
      isDoors: false,
      isRun: false,
    }
  },
  props: ['elevator', 'floors', 'stack', 'current'],
  methods: {
    startElevator() {
      this.prev = this.current;
      this.time = +`${Math.abs(this.current - this.stack[0])}000`;
      this.isDoors = true;

      localStorage.setItem('prev', this.prev);
      localStorage.setItem('time', this.time);

      let t = setInterval(() => {
        this.isDoors = false;
        this.isRun = true;
        this.$emit('changeCurrent', this.stack[0]);
        clearInterval(t);

        let nextFloorT = setInterval(() => {
          clearInterval(nextFloorT);
          this.isRun = false;
          this.$emit('changeStack');
          if (this.stack.length > 1)  this.startElevator();
        }, this.time);
      }, 3000);
    },
  },
  mounted() {
    if (this.stack.length > 0) {
      this.startElevator();
    }
  },
  watch: {
    stack: {
        handler() {
          if (this.stack.length === 1 && !this.isRun) {
            this.startElevator();
          }
        },
      deep: true
    }
  }
}
</script>

<style lang="scss" scoped>

  @keyframes blinker {
    50% {
      background-color: black;
    }
  }
  .floor {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 216px;
    height: 216px;
    border: solid 1px #fff;
    list-style: none;
    font-size: 24px;
  }
  .shaft {
    display: flex;
    flex-direction: column-reverse;
    position: relative;
  }
  .elevator {
    display: flex;
    justify-content: center;
    width: 216px;
    height: 216px;
    background-color: #6C766E;
    border: solid 1px #fff;
    position: absolute;
    transition-property: all;
    transition-timing-function: linear;
    background-image: url(../assets/elevator.jpg);
    background-repeat: no-repeat;
    background-position: center;
  }
  
  .elevator-animation {
    animation: blinker 1s linear infinite;
  }

  .floor__panel {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 5px;
    margin-top: 18px;
    width: 60px;
    height: 26px;
    background: #fff;
    border: solid 2px #1E1A20;
    border-radius: 4px;
  }

  .current-floor {
    font-size: 16px;
    line-height: 19px;
    color: #EE4F4F;
  }
  .floor__icon {
    width: 9px;
    height: 15px;
    background-repeat: no-repeat;
    background-size: contain;
    background-color: transparent;
    background-position: center;
  }

  .floor__up {
    background-image: url(../assets/up.svg);
  }
  .floor__down {
    background-image: url(../assets/down.svg);
  }
</style>