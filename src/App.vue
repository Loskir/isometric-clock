<template>
  <div id="app" :class="darkTheme ? 'black' : 'default'">
    <div class="svg-wrapper">
      <svg class="svg" viewBox="-10 -10 1020 1020">
        <defs>
          <linearGradient
            id="hours-seconds-gradient"
            :x1="hoursPointNT.x"
            :y1="hoursPointNT.y"
            :x2="secondsPointNT.x"
            :y2="secondsPointNT.y"
            gradientUnits="userSpaceOnUse">
            <stop :stop-color="hoursColor" offset="0"/>
            <stop :stop-color="secondsColor" offset="1"/>
          </linearGradient>
          <linearGradient
            id="minutes-seconds-gradient"
            :x1="minutesPointNT.x"
            :y1="minutesPointNT.y"
            :x2="secondsPointNT.x"
            :y2="secondsPointNT.y"
            gradientUnits="userSpaceOnUse">
            <stop :stop-color="minutesColor" offset="0"/>
            <stop :stop-color="secondsColor" offset="1"/>
          </linearGradient>
          <linearGradient
            id="hours-minutes-gradient"
            :x1="hoursPointNT.x"
            :y1="hoursPointNT.y"
            :x2="minutesPointNT.x"
            :y2="minutesPointNT.y"
            gradientUnits="userSpaceOnUse">
            <stop :stop-color="hoursColor" offset="0"/>
            <stop :stop-color="minutesColor" offset="1"/>
          </linearGradient>
        </defs>
        <VectorLine class="axle" :vector="hourAxleVector"/>
        <VectorLine class="axle" :vector="minuteAxleVector"/>
        <VectorLine class="axle" :vector="secondAxleVector"/>

        <polygon class="arrow" :points="hoursArrowPointString"/>
        <polygon class="arrow" :points="minutesArrowPointString"/>
        <polygon class="arrow" :points="secondsArrowPointString"/>

        <polygon :points="planePoints" class="plane"/>

        <line
          class="line"
          stroke="url(#hours-seconds-gradient)"
          :x1="hoursPointNT.x"
          :y1="hoursPointNT.y"
          :x2="secondsPointNT.x"
          :y2="secondsPointNT.y"/>
        <line
          class="line"
          stroke="url(#minutes-seconds-gradient)"
          :x1="minutesPointNT.x"
          :y1="minutesPointNT.y"
          :x2="secondsPointNT.x"
          :y2="secondsPointNT.y"/>
        <line
          class="line"
          stroke="url(#hours-minutes-gradient)"
          :x1="hoursPointNT.x"
          :y1="hoursPointNT.y"
          :x2="minutesPointNT.x"
          :y2="minutesPointNT.y"/>

        <text
          class="text"
          text-anchor="start"
          alignment-baseline="central"
          :x="hourAxleTextPointN.x"
          :y="hourAxleTextPointN.y">
          часы
        </text>
        <text
          class="text"
          text-anchor="end"
          :x="minuteAxleTextPointN.x"
          :y="minuteAxleTextPointN.y">
          минуты
        </text>
        <text
          class="text"
          text-anchor="start"
          :x="secondAxleTextPointN.x"
          :y="secondAxleTextPointN.y">
          секунды
        </text>

        <circle class="point" :stroke="hoursColor" r="7" :cx="hoursPointNT.x" :cy="hoursPointNT.y"/>
        <circle class="point" :stroke="minutesColor" r="7" :cx="minutesPointNT.x" :cy="minutesPointNT.y"/>
        <circle class="point" :stroke="secondsColor" r="7" :cx="secondsPointNT.x" :cy="secondsPointNT.y"/>

        <text
          class="text"
          text-anchor="end"
          :x="hoursTextPointNT.x"
          :y="hoursTextPointNT.y">
          {{hour}}
        </text>
        <text
          class="text"
          text-anchor="start"
          :x="minutesTextPointNT.x"
          :y="minutesTextPointNT.y">
          {{minute}}
        </text>
        <text
          class="text"
          text-anchor="end"
          :x="secondsTextPointNT.x"
          :y="secondsTextPointNT.y">
          {{second}}
        </text>
      </svg>
    </div>
    <footer class="footer">
      <span>Made with ❤️ by <a href="https://loskir.ru" target="_blank">@Loskir</a></span>
      <span><a href="https://github.com/Loskir/isometric-clock" target="_blank">GitHub</a></span>
    </footer>

    <div class="settings">
      <label class="switch settings__item">
        <span class="switch__label">Theme</span>
        <input class="switch__input" type="checkbox" v-model="darkTheme"/>
        <div class="switch__content">
          <div class="switch__content-inner">
            <svg class="switch__content-inner-svg" v-if="darkTheme" viewBox="0 0 312.812 312.812">
              <path d="M305.2,178.159c-3.2-0.8-6.4,0-9.2,2c-10.4,8.8-22.4,16-35.6,20.8c-12.4,4.8-26,7.2-40.4,7.2c-32.4,0-62-13.2-83.2-34.4
                c-21.2-21.2-34.4-50.8-34.4-83.2c0-13.6,2.4-26.8,6.4-38.8c4.4-12.8,10.8-24.4,19.2-34.4c3.6-4.4,2.8-10.8-1.6-14.4
                c-2.8-2-6-2.8-9.2-2c-34,9.2-63.6,29.6-84.8,56.8c-20.4,26.8-32.4,60-32.4,96c0,43.6,17.6,83.2,46.4,112s68,46.4,112,46.4
                c36.8,0,70.8-12.8,98-34c27.6-21.6,47.6-52.4,56-87.6C314,184.959,310.8,179.359,305.2,178.159z"/>
            </svg>
            <svg class="switch__content-inner-svg" v-else viewBox="0 0 45.16 45.16">
              <path
                d="M22.58,11.269c-6.237,0-11.311,5.075-11.311,11.312s5.074,11.312,11.311,11.312c6.236,0,11.311-5.074,11.311-11.312 S28.816,11.269,22.58,11.269z"/>
              <path
                d="M22.58,7.944c-1.219,0-2.207-0.988-2.207-2.206V2.207C20.373,0.988,21.361,0,22.58,0c1.219,0,2.207,0.988,2.207,2.207 v3.531C24.787,6.956,23.798,7.944,22.58,7.944z"/>
              <path
                d="M22.58,37.215c-1.219,0-2.207,0.988-2.207,2.207v3.53c0,1.22,0.988,2.208,2.207,2.208c1.219,0,2.207-0.988,2.207-2.208 v-3.53C24.787,38.203,23.798,37.215,22.58,37.215z"/>
              <path
                d="M32.928,12.231c-0.861-0.862-0.861-2.259,0-3.121l2.497-2.497c0.861-0.861,2.259-0.861,3.121,0 c0.862,0.862,0.862,2.26,0,3.121l-2.497,2.497C35.188,13.093,33.791,13.093,32.928,12.231z"/>
              <path
                d="M12.231,32.93c-0.862-0.863-2.259-0.863-3.121,0l-2.497,2.496c-0.861,0.861-0.862,2.26,0,3.121 c0.862,0.861,2.26,0.861,3.121,0l2.497-2.498C13.093,35.188,13.093,33.79,12.231,32.93z"/>
              <path
                d="M37.215,22.58c0-1.219,0.988-2.207,2.207-2.207h3.531c1.219,0,2.207,0.988,2.207,2.207c0,1.219-0.988,2.206-2.207,2.206 h-3.531C38.203,24.786,37.215,23.799,37.215,22.58z"/>
              <path
                d="M7.944,22.58c0-1.219-0.988-2.207-2.207-2.207h-3.53C0.988,20.373,0,21.361,0,22.58c0,1.219,0.988,2.206,2.207,2.206 h3.531C6.956,24.786,7.944,23.799,7.944,22.58z"/>
              <path
                d="M32.928,32.93c0.862-0.861,2.26-0.861,3.121,0l2.497,2.497c0.862,0.86,0.862,2.259,0,3.12s-2.259,0.861-3.121,0 l-2.497-2.497C32.066,35.188,32.066,33.791,32.928,32.93z"/>
              <path
                d="M12.231,12.231c0.862-0.862,0.862-2.259,0-3.121L9.734,6.614c-0.862-0.862-2.259-0.862-3.121,0 c-0.862,0.861-0.862,2.259,0,3.12l2.497,2.497C9.972,13.094,11.369,13.094,12.231,12.231z"/>
            </svg>

          </div>
        </div>
      </label>
    </div>
  </div>
</template>

<script>
  import VectorLine from '@/components/VectorLine.vue'
  import PointCircle from '@/components/Point.vue'

  const clockRadius = 500

  class Point {
    constructor(x, y) {
      this.x = x
      this.y = y
    }
    add(point) {
      return new Point(this.x + point.x, this.y + point.y)
    }
    normalize() {
      return new Point(clockRadius + this.x, clockRadius + 100 - this.y)
    }
    moveBy(angle, distance) {
      const {sin, cos} = Math
      return new Point(this.x + distance * sin(angle), this.y + distance * cos(angle))
    }
    toArray() {
      return [this.x, this.y]
    }
    toPointString() {
      return `${this.x},${this.y}`
    }

    static fromTweened(point) {
      return new Point(point.x, point.y)
    }
  }

  class Vector {
    constructor(start, end) {
      this.start = start
      this.end = end
    }
    get x() {
      return this.end.x - this.start.x
    }
    get y() {
      return this.end.y - this.start.y
    }
  }

  function rebound(v, a1, b1, a2, b2) {
    // a1[...v....]b1
    //     to
    // a2[...u....]b2
    const l1 = b1 - a1
    const l2 = b2 - a2
    return a2 + (v - a1) / l1 * l2
  }

  export default {
    name: 'app',
    components: {
      VectorLine,
      PointCircle,
    },
    data() {
      return {
        clockRadius,
        axisLength: 550,
        fullRadius: 480,
        secondRadius: 380,
        minuteRadius: 370,
        hourRadius: 230,
        centerRadius: 100,
        pointLength: 100,
        slowAnimationDuration: 2000,
        fastAnimationDuration: 500,

        notchOuter: 470,
        notchInner: 420,
        numbersRadius: 500,

        ms: 0,

        darkTheme: false,

        Point,
        Vector,

        numberAngles: [],

        hoursColor: '#6d268c',
        minutesColor: '#e5be40',
        secondsColor: '#d4006e',
      }
    },
    methods: {
      updateTime() {
        const date = new Date()
        this.ms = Date.now() % 86400000 - date.getTimezoneOffset() * 60000

        setTimeout(() => this.updateTime(), 1000 - date.getMilliseconds())
      },

      getTextPosition(index) {
        const angle = index / 60 * 2 * Math.PI
        const r = this.numbersRadius
        return new Point(r * Math.sin(angle), r * Math.cos(angle))
      },
      getNumberPosition(angle) {
        const r = this.numbersRadius
        return new Point(r * Math.sin(angle), r * Math.cos(angle))
      },

      getFancyRotatingAngle(oldValue, newValue) {
        const pi2 = (Math.PI * 2)
        const angleNormalized = (oldValue % pi2 + pi2) % pi2
        const fullTurns = Math.floor(oldValue / pi2)
        if (angleNormalized - newValue > Math.PI) {
          return (fullTurns + 1) * pi2 + newValue
        }
        if (newValue - angleNormalized > Math.PI) {
          return (fullTurns - 1) * pi2 + newValue
        }
        return fullTurns * pi2 + newValue
      },

      getArrowPointString(baseAngle) {
        const head = new Point(0, 0).moveBy(baseAngle, this.axisLength)
        const l = head.moveBy(baseAngle + Math.asin(3/10), -10)
        const m = head.moveBy(baseAngle, -7)
        const r = head.moveBy(baseAngle - Math.asin(3/10), -10)
        return `${l.normalize().toPointString()} ${head.normalize().toPointString()} ${r.normalize().toPointString()} ${m.normalize().toPointString()}`
      },
    },
    computed: {
      second() {
        return Math.floor(this.ms / 1000 % 60)
      },
      minute() {
        return Math.floor(this.ms / 60000 % 60)
      },
      hour() {
        return Math.floor(this.ms / 3600000 % 24)
      },

      hourAxleEndPoint() {
        return new Point(0, this.axisLength)
      },
      minuteAxleEndPoint() {
        return new Point(0, 0).moveBy(2 * Math.PI / 3, this.axisLength)
      },
      secondAxleEndPoint() {
        return new Point(0, 0).moveBy(4 * Math.PI / 3, this.axisLength)
      },

      hourAxleVector() {
        return new Vector(new Point(0, 0), this.hourAxleEndPoint)
      },
      minuteAxleVector() {
        return new Vector(new Point(0, 0), this.minuteAxleEndPoint)
      },
      secondAxleVector() {
        return new Vector(new Point(0, 0), this.secondAxleEndPoint)
      },

      hourPoint() {
        return new Point(0, 0).moveBy(
          0,
          rebound(this.hour, 0, 23, 70, this.fullRadius)
        )
      },
      minutePoint() {
        return new Point(0, 0).moveBy(
          2 * Math.PI / 3,
          rebound(this.minute, 0, 59, 70, this.fullRadius)
        )
      },
      secondPoint() {
        return new Point(0, 0).moveBy(
          4 * Math.PI / 3,
          rebound(this.second, 0, 59, 70, this.fullRadius)
        )
      },

      planePoints() {
        const hn = Point.fromTweened(this.hoursPointNT)
        const mn = Point.fromTweened(this.minutesPointNT)
        const sn = Point.fromTweened(this.secondsPointNT)

        return `${hn.toPointString()} ${mn.toPointString()} ${sn.toPointString()}`
      },

      hourTextPoint() {
        return this.hourPoint.add(new Point(-15, 0))
      },
      minuteTextPoint() {
        return this.minutePoint.add(new Point(5, 15))
      },
      secondTextPoint() {
        return this.secondPoint.add(new Point(-5, 15))
      },

      hoursArrowPointString() {
        return this.getArrowPointString(0)
      },
      minutesArrowPointString() {
        return this.getArrowPointString(2 * Math.PI / 3)
      },
      secondsArrowPointString() {
        return this.getArrowPointString(4 * Math.PI / 3)
      },

      hourAxleTextPoint() {
        return this.hourAxleEndPoint.add(new Point(10, 0))
      },
      minuteAxleTextPoint() {
        return this.minuteAxleEndPoint.add(new Point(-25, -10))
      },
      secondAxleTextPoint() {
        return this.secondAxleEndPoint.add(new Point(25, -10))
      },

      hourAxleTextPointN() {
        return this.hourAxleTextPoint.normalize()
      },
      minuteAxleTextPointN() {
        return this.minuteAxleTextPoint.normalize()
      },
      secondAxleTextPointN() {
        return this.secondAxleTextPoint.normalize()
      },
    },
    tweened: {
      hoursPointNT: {
        get() {
          return this.hourPoint.normalize()
        },
        duration: () => 100,
        easing: (t) => t * (2 - t),
      },
      minutesPointNT: {
        get() {
          return this.minutePoint.normalize()
        },
        duration: () => 100,
        easing: (t) => t * (2 - t),
      },
      secondsPointNT: {
        get() {
          return this.secondPoint.normalize()
        },
        duration: () => 100,
        easing: (t) => t * (2 - t),
      },

      hoursTextPointNT: {
        get() {
          return this.hourTextPoint.normalize()
        },
        duration: () => 100,
        easing: (t) => t * (2 - t),
      },
      minutesTextPointNT: {
        get() {
          return this.minuteTextPoint.normalize()
        },
        duration: () => 100,
        easing: (t) => t * (2 - t),
      },
      secondsTextPointNT: {
        get() {
          return this.secondTextPoint.normalize()
        },
        duration: () => 100,
        easing: (t) => t * (2 - t),
      },
    },
    watch: {},
    mounted() {
      this.updateTime()
    }
  }
</script>

<style lang="stylus">
  *
    box-sizing border-box

  body
    margin 0

  .switch
    display flex
    flex-direction row
    align-items center

  .switch__input
    height 0
    width 0
    visibility hidden
    margin 0
    position absolute

  .switch__label
    padding-right 5px

  .switch__content
    cursor pointer
    width 40px
    height 21px
    display block
    border-radius 100px
    position relative

  .switch__content-inner
    position absolute
    top 3px
    left 3px
    width 15px
    height 15px
    border-radius 90px
    transition left .3s, transform .3s, width .3s

    display flex
    flex-direction row
    justify-content center

  .switch__content-inner-svg
    padding 2px
    width 100%
    height 100%

  .switch__input:checked + .switch__content .switch__content-inner
    left calc(100% - 3px)
    transform translateX(-100%)

  .switch:active .switch__content-inner
    width 20px

  #app
    font-family Ubuntu, monospace
    font-style italic
    display flex
    flex-direction column
    justify-content center
    align-items center
    height 100vh
    overflow hidden

  a
    color #007bff
    text-decoration none
    transition .2s

    &:hover
      color #0056b3

  .svg-wrapper
    width 100%
    height 100%
    box-sizing border-box

  .svg
    max-width 100%
    max-height 100%

    .arrow
      stroke-linecap round

    .axle
      stroke-width 1

    .hour-arrow
      stroke-width 7

    .minute-arrow
      stroke-width 5

    .second-arrow
      stroke-width 2

    .notch
      stroke-linecap round
      stroke-width 7

    .text
      font-size 24px

    .plane
      stroke none

    .point, .line
      stroke-width 1.5

  .footer
    position absolute
    z-index 100
    width 100%
    bottom 0
    padding 15px 50px
    box-sizing border-box
    display flex
    flex-direction row
    justify-content space-between

  .settings
    position fixed
    right 0
    top 0
    padding 10px
    display flex
    flex-direction column
    align-items flex-end

  .settings__item
    font-size 13px

    &:not(:last-child)
      padding-bottom 5px

  select
    font-family monospace
    border none

  .default
    .svg
      .arrow, .axle
        stroke #1f1f1f

      .arrow
        fill #1f1f1f

      .text
        fill #1f1f1f

      .point
        fill white

      .plane
        fill #ffffffc0

    .footer
      background white

    .switch__content
      background black

    .switch__content-inner
      background #fff

    .switch__content-inner-svg
      fill black

  .black
    background-color black
    color white

    .svg
      .arrow, .axle
        stroke white

      .arrow, .text
        fill white

      .axle
        stroke-width 1.3

      .point
        fill black

      .plane
        fill #000000a0

    .footer
      background black

    .switch__content
      background white

    .switch__content-inner
      background black

    .switch__content-inner-svg
      fill white

    select
      background-color black
      color white
</style>
