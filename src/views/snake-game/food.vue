<template>
  <div class="food" :style="{'left': food[0]+'%', 'top': food[1]+'%'}"></div>
</template>

<script>
export default {
  name: "Food",
  props: {
    food: {
      type: Array,
      default: () => [],
    }
  },
  setup (props, context) {

    return {}
  }
}
</script>

<style lang="scss" scoped>
.food {
  position: absolute;
  width: 2%;
  height: 2%;
  background: red;
  border: 1px solid #fff;
}
</style>