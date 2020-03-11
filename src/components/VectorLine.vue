<template>
  <line
    :x1="vector.start.normalize().x"
    :y1="vector.start.normalize().y"
    :x2="vector.end.normalize().x"
    :y2="vector.end.normalize().y"/>
</template>

<script>
  export default {
    name: 'VectorLine',
    props: {
      vector: Object,
    },
    data: () => ({
      clockRadius: 500,
      secondRadius: 300,
      minuteRadius: 200,
      hourRadius: 100,
    }),
    methods: {
      normalizeX(x) {
        return this.clockRadius+x
      },
      normalizeY(y) {
        return this.clockRadius-y
      },
    }
  }
</script>

<style scoped lang="stylus">

</style>