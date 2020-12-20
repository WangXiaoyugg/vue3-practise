<template>
  <div class="snake-game">
    <h1 class="snake-game__title">Snake Game</h1>
    <div class="snake-game__area">
      <Snake :body="body"></Snake>
      <Food :food="food"></Food>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'
import Snake from './snake.vue'
import Food from './food.vue'

const generateRandomCoordinates = () => {
  let min = 1;
  let max = 49;
  let x = Math.floor(Math.random() * max + min) * 2;
  let y = Math.floor(Math.random() * max + min) * 2;
  return [x, y]
}

export default {
  name: 'SnakeGame',
  components: {
    Snake,
    Food,
  },
  setup() {
    const foodCoordinates = generateRandomCoordinates()
    const body = ref([
      [0, 0],
      [2, 0],
    ]);
    const direction = ref('RIGHT');
    const food = ref(foodCoordinates);
    const speed = ref(200);
    const onKeyDown = ({keyCode}) => {
      switch (keyCode) {
        case 38:
          direction.value = 'UP';
          break;
        case 40:
          direction.value = 'DOWN';
          break;
        case 37:
          direction.value = 'LEFT';
          break;
        case 39:
          direction.value = 'RIGHT';
          break;
        default: 
          direction.value = 'RIGHT';  
      }
    }
    const moveSnake = () => {
      let originBody = [...body.value];
      let head = originBody[originBody.length -1];
      let step = 2;
      switch (direction.value) {
        case 'UP':
          head = [head[0], head[1] - step]
          break;
        case 'DOWN':
          head = [head[0], head[1] + step]
          break;
        case 'LEFT':
          head = [head[0] - step, head[1]]
          break;
        case 'RIGHT':
          head = [head[0] + step, head[1]]
          break;
        default: 
          head = [head[0] + step, head[1]]
      }
      originBody.push(head)
      originBody.shift()
      body.value = originBody
    }
    document.addEventListener('keydown', onKeyDown)
    setInterval(moveSnake, speed.value)

  
    return {
      body,
      food,
    }

  }
}
</script>

<style lang="scss" scoped>
.snake-game  {
  display: flex;
  flex-direction: column;
  align-items: center;
  &__title {
    font-weight: bold;
    font-style: italic;
  }
  &__area {
    border: 1px solid #000;
    width: 600px;
    height: 600px;
    position: relative;
  }
}
</style>