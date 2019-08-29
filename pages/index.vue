<template lang="pug">
  main.main
    .content
      h1.title
        nuxt-link(to="/", aria-label="HIGHER")
          Logo

      .wrap
        p.copy
          span #[span Hi. My name is Taka.]
          span #[span I’m Designer and Developer]
          span #[span based in Tokyo.]
        ul.lists
          li.list
            a(href="https://dribbble.com/intkaaa", target="_blank", rel="noopener") dribbble.com#[span /intkaaa]
          li.list
            a(href="https://twitter.com/intkaaa", target="_blank", rel="noopener") twitter.com#[span /intkaaa]
          li.list
            a(href="https://note.mu/intkaaa", target="_blank", rel="noopener") note.mu#[span /intkaaa]

      .contact
        span
          a(href="https://m.me/intkaaa", target="_blank", rel="noopener") Say hi. #[img(src="/messenger.svg", alt="messenger")]
</template>

<script>
import Logo from '~/components/Logo.vue'

export default {
  components: {
    Logo
  },
  mounted() {
    this.$nextTick(() => {
      setTimeout(function() {
        document.body.classList.add('loaded')
      }, 1000)

      const viewportUnitsBuggyfill = require('viewport-units-buggyfill')
      viewportUnitsBuggyfill.init()

      let height = window.innerHeight
      document.querySelector('.main').style.height = height + 'px'
    })
  }
}
</script>

<style lang="stylus">
.main
  width 75%
  height 100%
  padding 80px 0
  margin auto
  +tl()
    width 80%
    padding 10.6666vw 0

  .title
    overflow hidden
    a
      display inline-block
      opacity 0
      transform translateY(105%) translateZ(0)
      transition transform .8s cubic-bezier(.165,.84,.44,1) .6s

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

      .copy
        margin-top -8%
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
          font-size 6.2vw
          line-height 152%
        > span
          display block
          overflow hidden
          > span
            display block
            opacity 0
            transform translateY(105%) translateZ(0)
            transition transform .8s cubic-bezier(.165,.84,.44,1) .6s

      .lists
        margin-top 40px
        +tl()
          margin-top 32px
        +sp()
          margin-top 20px

        .list
          margin-top 24px
          overflow hidden
          +tl()
            margin-top 18px
          +sp()
            margin-top 12px
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
            color base
            font-family museo-sans
            font-size 2vh
            line-height 1
            letter-spacing .04rem
            opacity 0
            transform translateY(110%) translateZ(0)
            transition transform .8s cubic-bezier(.165,.84,.44,1)
            +tl()
              font-size 1.5625vw
            +sp()
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
        transition transform .8s cubic-bezier(.165,.84,.44,1) 1.1s
      a
        display flex
        align-items center
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
</style>
