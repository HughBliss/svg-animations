<template>
  <div class="container">
    <rotating-sun />
    <dancing-worm :rotate="50" />
  </div>
</template>
<script>
import DancingWorm from '~/components/animated-shapes/DancingWorm'
import RotatingSun from '~/components/animated-shapes/RotatingSun'

export default {
  components: {
    RotatingSun,
    DancingWorm
  }
}
</script>
