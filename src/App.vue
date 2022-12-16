<template>
  <main>
    <div class="container">
      <MainElevator 
        v-for="elevator in elevators"
        :key="elevator" 
        :elevator="elevator" 
        :floors="floors"
      />
    </div>
  </main>
</template>

<script>
import MainElevator from './components/MainElevator.vue';

export default {
  data() {
    return {
      elevators: 1,
      floors: 5,
      stack: [],
    }
  },
  components: { MainElevator },
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

</style>
