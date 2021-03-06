<template>
  <svg width="124" height="600" viewBox="0 0 124 600" fill="none" xmlns="http://www.w3.org/2000/svg">
    <path
      ref="path"
      d=""
      stroke="#4F4F4F"
      :stroke-width="strokeWidth"
      stroke-linecap="round"
    />
  </svg>
</template>

<script>
import { segments } from '~/components/animated-shapes/SpringSnakeSprite'

export default {
  name: 'SpringSnake',
  props: {
    strokeWidth: {
      default: 4,
      type: Number
    }
  },
  data () {
    const keyframes = []
    const strokeFactor = this.strokeWidth / 2

    for (let i = 0; i < 150; i++) {
      const lastSegmentIndex = (i + 9) % 10
      const lastFactor = (((i + 9) / 10) | 0) - 1
      let path = `path('M ${segments[lastSegmentIndex].dot[0] + strokeFactor} ${segments[lastSegmentIndex].dot[1] + (30 * lastFactor) + strokeFactor}`
      for (let j = i; j < i + 30; j++) {
        const segment = segments[j % 10]
        const factor = (j / 10) | 0
        path += `C ${segment.rail1[0] + strokeFactor} ${segment.rail1[1] + 30 * factor + strokeFactor} \
              ${segment.rail2[0] + strokeFactor} ${segment.rail2[1] + 30 * factor + strokeFactor} \
              ${segment.dot[0] + strokeFactor} ${segment.dot[1] + 30 * factor + strokeFactor}`
      }
      keyframes.push({ d: path })
    }
    return {
      keyframes
    }
  },
  mounted () {
    this.$refs.path.animate(this.keyframes, {
      duration: 2500,
      direction: 'alternate',
      iterations: Infinity
    })
  }
}
</script>

<style scoped>
svg {
  transform: rotate(-45deg);
}
</style>
