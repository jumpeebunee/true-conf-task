<template>
  <main>
    <div class="container">
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      elevators: 1,
      floors: 5,
      stack: [],
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

</style>
