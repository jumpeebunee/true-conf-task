<template>
    <div class="shaft">
        <li v-for="floor in floors" :key="floor" class="floor"></li>
        <div
            :style="{'bottom': `${(current - 1)* 216}px`,
            'transition-duration': `${time.toString()[0]}s`}"
            :class="{'elevator elevator-animation': isDoors, 'elevator': !isDoors}"
        >
          <div class="floor__panel">
            <div v-show="isRun" class="floor__panel-content">
              <div class="floor__icon floor__up" v-if="prev < current"></div>
              <div class="floor__icon floor__down" v-else></div>
              <div class="current-floor">{{current}}</div>
            </div>
          </div>
        </div>
    </div>
</template>

<script>
export default {
  data() {
    return {
      current: 1,
      prev: 0,
      time: 3000,
      isDoors: false,
      isRun: false,
    }
  },
  props: ['elevator', 'floors',],
}
</script>

<style lang="scss" scoped>

  @keyframes blinker {
    50% {
      opacity: 0;
    }
  }
  .floor {
    width: 216px;
    height: 216px;
    border: solid 1px #fff;
    list-style: none;
  }

  .shaft {
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
    margin-top: 18px;
    width: 60px;
    height: 26px;
    background: #fff;
    border: solid 2px #1E1A20;
    border-radius: 4px;
  }

  .floor__panel-content {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 5px;
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