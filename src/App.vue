<template>
  <main>
    <div class="container">
      <div class="elevator__content">
        <MainElevator 
          v-for="elevator in elevators"
          @changeQueue="changeQueue"
          @changeCurrent="changeCurrent"
          :current="current"
          :elevator="elevator" 
          :floors="floors"
          :queue="queue"
          :key="elevator" 
        />
        <MainButtons
          @pushToQueue="pushToQueue"
          :queue="queue"
          :floors="floors"
        />
      </div>
      <ChangeFloors 
        @addFloor="addFloor"
        @removeFloor="removeFloor"
        :unActive="unActive"
        :floors="floors"
        :current="current"
      />
    </div>
  </main>
</template>

<script>
import MainElevator from './components/MainElevator.vue';
import MainButtons from './components/MainButtons.vue';
import ChangeFloors from './components/ChangeFloors.vue';

export default {
  data() {
    return {
      elevators: 1,
      floors: +localStorage.getItem('floors') || 5,
      queue: JSON.parse(localStorage.getItem('queue')) || [],
      current: +localStorage.getItem('current') || 1,
      unActive: false,
    }
  },
  components: { MainElevator, MainButtons, ChangeFloors },
  methods: {
    changeQueue() {
      this.queue.shift();
      localStorage.setItem('queue', JSON.stringify(this.queue));
      if (this.queue.length === 0) this.unActive = false;
    },
    pushToQueue(val) {
      if (this.current === val || this.queue.includes(val)) return;
      this.unActive = true;
      this.queue.push(val);
      localStorage.setItem('queue', JSON.stringify(this.queue));
    },
    changeCurrent(val) {
      this.current = val;
      localStorage.setItem('current', this.current);
    },
    addFloor() {
      if (this.floors >= 30) {
        alert('Слишком много этажей :)');
        return;
      }
      this.floors += 1;
      localStorage.setItem('floors', this.floors);
    },
    removeFloor() {
      if (this.floors === this.current) return;
      this.floors -= 1;
      localStorage.setItem('floors', this.floors);
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
    align-items: center;
  }

  .elevator__content {
    display: flex;
    align-items: center;
  }


</style>
