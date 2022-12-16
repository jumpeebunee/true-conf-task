<template>
  <ul class="btns__list">
    <li v-for="floor in floors" :key="floor">
      <button @click="pushToQueue(floor)"><div class="btns__list-btn" :class="{'btns__list-btn active': queue.includes(floor)}"></div></button>
    </li>
  </ul>
</template>

<script>
export default {
  props: ['queue', 'floors'],
  methods: {
    pushToQueue(val) {
      this.$emit('pushToQueue', val);
    }
  }
}
</script>

<style lang="scss" scoped>
  .btns__list {
    display: flex;
    flex-direction: column-reverse;

    li {
      display: flex;
      align-items: center;
      justify-content: center;
      width: 79px;
      height: 216px;
      border: solid 1px #fff;
    }

    button {
      display: flex;
      align-items: center;
      justify-content: center;
      width: 30px;
      height: 44px;
      background: transparent;
      border: solid 1px #fff;
      border-radius: 4px;
    }

    .btns__list-btn {
      width: 10px;
      height: 10px;
      border-radius: 50%;
      border: solid 1px #fff;
    }
    .active {
      background-color: #EE4F4F;
    }

  }
</style>