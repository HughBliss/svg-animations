<template>
  <div class="container">
    <rotating-sun />
    <dancing-worm :rotate="50" />
    <spring-snake />
  </div>
</template>
<script>

import DancingWorm from '~/components/animated-shapes/DancingWorm'
import SpringSnake from '~/components/animated-shapes/SpringSnake'
import RotatingSun from '~/components/animated-shapes/RotatingSun'

export default {
  components: {
    RotatingSun,
    DancingWorm,
    SpringSnake
  }
}
</script>
