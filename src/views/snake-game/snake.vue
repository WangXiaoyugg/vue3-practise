<template>
  <div 
    class="snake" 
    v-for="item in body"
    :style="{'left': item[0]+'%', 'top': item[1]+'%'}"></div>
</template>

<script>
export default {
  name: 'Snake',
  props: {
    body: {
      type: Array,
      default: () => [],
    }
  }
}
</script>

<style lang="scss" scoped>
.snake {
  position: absolute;
  width: 2%;
  height: 2%;
  background: #000;
  border: 1px solid #fff;
}
</style>