<template>
  <div class="elevator__description">
    <h1>Эмулятор Лифта</h1>
    <p>Дополнительные лифты добавить нельзя, но можно добавить количесто этажей</p>
    <div class="elevator__description-btns">
      <button @click="this.$emit('addFloor')">+</button>
      <button :class="{'unActive': unActive || floors === 1}" :disabled="unActive || floors === 1" @click="this.$emit('removeFloor')">-</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {}
  },
  props: ['floors', 'unActive'],
} 
</script>

<style lang="scss" scoped>
.elevator__description {
    margin-left: 200px;

    h1 {
      font-weight: 700;
      font-size: 64px;
      line-height: 77px;
    }
    p {
      margin-top: 15px;
      max-width: 500px;
      font-size: 18px;
      line-height: 22px;
      color: rgba(255, 255, 255, 0.8);
    }
  }
  .elevator__description-btns {
    display: flex;
    gap: 15px;
    margin-top: 20px;

    button {
      display: flex;
      align-items: center;
      justify-content: center;
      width: 50px;
      height: 50px;
      background: #EE4F4F;
      border-radius: 4px;
      font-weight: 700;
      font-size: 24px;
      line-height: 29px;
      color: #FFFFFF;
      transition: background .4s ease;
    }

    .unActive {
      background: #973B3C;
    }
  }

</style>