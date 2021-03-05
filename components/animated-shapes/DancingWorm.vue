<template>
  <svg
    ref="worm"
    width="22"
    height="550"
    viewBox="0 0 22 550"
    fill="none"
    xmlns="http://www.w3.org/2000/svg"
  >
    <path
      ref="wormPath"
      d=""
      stroke="#4F4F4F"
      stroke-width="4"
      stroke-miterlimit="10"
      stroke-linecap="round"
    />
    <!--    <path d="M10.5 1.5L10.5 268.5" stroke="#4F4F4F" stroke-width="3" stroke-miterlimit="10" stroke-linecap="round" />-->
  </svg>
</template>

<script>
export default {
  name: 'DancingWorm',
  props: {
    rotate: {
      default: 0,
      type: Number
    }
  },
  created () {
    if (process.browser) {
      // eslint-disable-next-line nuxt/no-globals-in-created
      window.addEventListener('mousemove', this.animate)
    }
  },
  mounted () {
    this.$refs.worm.style.transform = `rotate(${this.rotate}deg)`
    this.$refs.wormPath.style.transition = '.3s'
  },
  destroyed () {
    if (process.browser) {
      window.removeEventListener('mousemove', this.animate)
    }
  },
  methods: {
    animate (e) {
      if (process.browser) {
        const coefficient = (((e.pageX - e.pageY) / 100) | 0) + 7

        let path = `path("M 12,${coefficient * 10 + 2} `

        for (let j = 1; j <= 20; j += 4) {
          const i = j + coefficient
          if (coefficient % 2) {
            path += `Q -5, ${(i + 0) * 10 + 2} 12, ${(i + 1) * 10 + 2} `
            path += `Q 25, ${(i + 2) * 10 + 2} 12, ${(i + 3) * 10 + 2} `
          } else {
            path += `Q 25, ${(i + 0) * 10 + 2} 12, ${(i + 1) * 10 + 2} `
            path += `Q -5, ${(i + 2) * 10 + 2} 12, ${(i + 3) * 10 + 2} `
          }
        }
        path += '")'
        this.$refs.wormPath.style.d = path
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.worm {

  path {
    transition: all .3s;
  }

}
</style>
