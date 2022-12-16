<template>
  <main>
    <div class="container">
      <MainElevator 
        v-for="elevator in elevators"
        @changeStack="changeStack"
        @changeCurrent="changeCurrent"
        :current="current"
        :elevator="elevator" 
        :floors="floors"
        :stack="stack"
        :key="elevator" 
      />
      <MainButtons
        @pushToStack="pushToStack"
        :stack="stack"
        :floors="floors"
      />
    </div>
  </main>
</template>

<script>
import MainElevator from './components/MainElevator.vue';
import MainButtons from './components/MainButtons.vue';

export default {
  data() {
    return {
      elevators: 1,
      floors: 5,
      stack: [],
      current: 1,
    }
  },
  components: { MainElevator, MainButtons },
  methods: {
    changeStack() {
      this.stack.shift();
    },
    changeCurrent(val) {
      this.current = val;
    },
    pushToStack(val) {
      if (this.current === val || this.stack.includes(val)) return;
      this.stack.push(val);
    }
  }
}
</script>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=Lato:wght@300;400;700;900&display=swap');
  
  * {
    font-family: Inter;
    color: #fff;
  }

  body {
    background-color: #1E1A20;
  }

  .container  {
    display: flex;
  }


</style>
