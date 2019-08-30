<template lang="pug">
  .container(@mousemove="onMouseMove")
    .cursor(ref="cursor") #[.pointer]
    main.main
      .content
        h1.title(@mouseenter="mouseEnter", @mouseleave="mouseLeave")
          a(href="/", aria-label="HIGHER")
            Logo

        .wrap
          p.copy
            span #[span Hi. My name is Taka.]
            span #[span I’m a designer and developer]
            span #[span based in Tokyo.]
          ul.lists
            li.list
              a(href="https://dribbble.com/intkaaa", target="_blank", rel="noopener", @mouseenter="mouseEnter", @mouseleave="mouseLeave") dribbble.com#[span /intkaaa]
            li.list
              a(href="https://twitter.com/intkaaa", target="_blank", rel="noopener", @mouseenter="mouseEnter", @mouseleave="mouseLeave") twitter.com#[span /intkaaa]
            li.list
              a(href="https://note.mu/intkaaa", target="_blank", rel="noopener", @mouseenter="mouseEnter", @mouseleave="mouseLeave") note.mu#[span /intkaaa]

        .contact
          span
            a(href="https://m.me/intkaaa", target="_blank", rel="noopener", @mouseenter="mouseEnter", @mouseleave="mouseLeave") Say hi. #[img(src="/messenger.svg", alt="messenger")]
</template>

<script>
import Logo from '~/components/Logo.vue'

export default {
  components: {
    Logo
  },

  data() {
    return {
      cursorWidth: 26,
      mouseX: 0,
      mouseY: 0
    }
  },

  mounted() {
    this.$nextTick(() => {
      setTimeout(function() {
        document.body.classList.add('loaded')
      }, 1000)
      setTimeout(function() {
        document.body.classList.add('pointer-active')
      }, 1800)

      // let height = window.innerHeight
      // document.querySelector('.main').style.height = height + 'px'

      const viewportUnitsBuggyfill = require('viewport-units-buggyfill')
      viewportUnitsBuggyfill.init()
    })
  },

  methods: {
    onMouseMove(e) {
      let cursorWidth = 50

      this.$refs.cursor.style.left = e.pageX - cursorWidth / 2 + 'px'
      this.$refs.cursor.style.top = e.pageY - cursorWidth / 2 + 'px'
    },
    mouseEnter() {
      this.$refs.cursor.classList.add('is-mouseenter')
    },
    mouseLeave() {
      this.$refs.cursor.classList.remove('is-mouseenter')
    }
  }
}
</script>

<style lang="stylus">
.container
  position relative
  cursor none

.cursor
  @media(hover: hover)
    position absolute
    top 0
    left 0
    &.is-mouseenter
      .pointer
        transform scale(0.3)
        background-color base
    .pointer
      width 50px
      height 50px
      border 1px solid white
      border-radius 50%
      cursor none
      posinter-events none
      transition .4s

.main
  width 75%
  height 100vh
  padding 80px 0
  margin auto
  +tl()
    width 84%
    padding 9.3333vw 0

  .title
    overflow hidden
    a
      display inline-block
      opacity 0
      transform translateY(105%) translateZ(0)
      transition .8s cubic-bezier(.165,.84,.44,1) .6s

  .content
    display flex
    flex-direction column
    align-items flex-start
    height 100%

    .wrap
      display flex
      flex-direction column
      justify-content center
      flex-grow 1
      width 100%

      .copy
        margin-top -5%
        color base
        font-family minion-pro-caption
        font-size 6vh
        line-height 128%
        letter-spacing .08rem
        transition .6s
        +tl()
          margin-top -18%
          font-size 5.98958vw
          line-height 140%
        +sp()
          font-size 6.8vw
          line-height 152%
          letter-spacing 0
        > span
          display block
          overflow hidden
          > span
            display block
            opacity 0
            transform translateY(105%) translateZ(0)
            transition .8s cubic-bezier(.165,.84,.44,1) .6s

      .lists
        margin-top 28px
        +tl()
          margin-top 24px
        +sp()
          margin-top 16px

        .list
          margin-top 4px
          overflow hidden
          +tl()
            margin-top 4px
          +sp()
            margin-top 4px
          &:nth-of-type(1)
            margin-top 0
            a
              transition-delay 0.8s
          &:nth-of-type(2)
            a
              transition-delay 0.9s
          &:nth-of-type(3)
            a
              transition-delay 1.1s
          a
            display inline-block
            padding 10px 0
            color base
            font-family museo-sans
            font-size 2vh
            line-height 1
            letter-spacing .04rem
            opacity 0
            transform translateY(110%) translateZ(0)
            transition .8s cubic-bezier(.165,.84,.44,1)
            +tl()
              font-size 1.5625vw
            +sp()
              padding 6px 0
              font-size 3.2vw
            span
              color base_pale
              transition .6s
            @media(hover: hover)
              &:hover
                span
                  color base

    .contact
      overflow hidden
      span
        display inline-block
        opacity 0
        transform translateY(105%) translateZ(0)
        transition .8s cubic-bezier(.165,.84,.44,1) 1.1s
      a
        display flex
        align-items center
        padding 10px 0
        color base_pale
        font-family museo-sans
        font-size 1.2rem
        line-height 1
        letter-spacing .04rem
        transition .6s
        +tl()
          font-size 1.5625vw
        +sp()
          font-size 3.2vw
        @media(hover: hover)
          &:hover
            color base
            img
              opacity 1
        img
          display inline-block
          width 0.8vw
          height auto
          margin-top -2px
          margin-left 4px
          transition .2s
          opacity 0

.loaded
  .title a,
  .copy > span > span,
  .list a,
  .contact span
    opacity 1 !important
    transform translateZ(0) !important

.pointer-active
  .pointer
    border-color base
</style>
