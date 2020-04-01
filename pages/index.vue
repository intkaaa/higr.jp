<template lang="pug">
  .container
    main.main
      .content
        h1.content__title.title
          a.title__wrap(href="/", aria-label="Higher")
            Logo

        .content__read.read
          p.read__copy.copy
            span.copy__row
              span.copy__text Hi. My name is Taka.
            span.copy__row
              span.copy__text I’m a designer and developer
            span.copy__row
              span.copy__text based in Tokyo.

          ul.read__lists.lists
            li.lists__list.list
              a.list__link(href="https://dribbble.com/intkaaa", target="_blank")
                span.list__service dribbble.com
                  span.list__account /intkaaa

            li.lists__list.list
              a.list__link(href="https://twitter.com/intkaaa", target="_blank")
                span.list__service twitter.com
                  span.list__account /intkaaa

            li.lists__list.list
              a.list__link(href="https://note.mu/intkaaa", target="_blank")
                span.list__service note.mu
                  span.list__account /intkaaa

        .content__contact.contact
          span.contact__wrap
            a.contact__link(href="https://m.me/intkaaa", target="_blank") Say hi.
              img.contact__icon(src="/messenger.svg", alt="messenger")
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
    })

    // DarkTheme
    if (window.matchMedia('(prefers-color-scheme: dark)').matches) {
      document.documentElement.setAttribute('data-mode', 'dark')
    }
    window.matchMedia('(prefers-color-scheme: dark)').addListener(e => {
      if (e.matches) {
        document.documentElement.setAttribute('data-mode', 'dark')
      } else {
        document.documentElement.setAttribute('data-mode', 'light')
      }
    })
  }
}
</script>

<style lang="stylus">
html
  color base
  background white
  &[data-mode="dark"]
    color dark_accent
    background dark_base

.container
  position relative
  &::before
    content ''
    position fixed
    top -100%
    left -50%
    width 300%
    height 300%
    opacity 0.2
    background-image url('/noise.png')
    animation grain 8s steps(10) infinite
    [data-mode="dark"] &
      opacity 0.015
      background-image url('/noise_invert.png')

@keyframes grain
  0%, 100% { transform:translate(0, 0) }
  10% { transform:translate(-5%, -10%) }
  20% { transform:translate(-15%, 5%) }
  30% { transform:translate(7%, -25%) }
  40% { transform:translate(-5%, 25%) }
  50% { transform:translate(-15%, 10%) }
  60% { transform:translate(15%, 0%) }
  70% { transform:translate(0%, 15%) }
  80% { transform:translate(3%, 35%) }
  90% { transform:translate(-10%, 10%) }

.main
  width 80%
  height 100vh
  padding 80px 0
  margin auto
  +tl()
    width 84%
    padding 9.3333vw 0

.content
  display flex
  flex-direction column
  align-items flex-start
  height 100%

.title
  overflow hidden
  &__wrap
    display inline-block
    // opacity 0
    // transform translateY(105%) translateZ(0)
    // transition .8s cubic-bezier(.165,.84,.44,1) .6s

.read
  display flex
  flex-direction column
  justify-content center
  flex-grow 1
  width 100%
  &__copy
    margin-top -1%
  &__lists
    margin-top 28px
    +tl()
      margin-top 24px
    +sp()
      margin-top 16px

.copy
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
  &__row
    display block
    overflow hidden
  &__text
    display block
    opacity 0
    transform translateY(105%) translateZ(0)
    transition .8s cubic-bezier(.165,.84,.44,1) .6s

.lists
  &__list
    margin-top 4px
    +tl()
      margin-top 4px
    +sp()
      margin-top 4px
    &:nth-of-type(1)
      margin-top 0

.list
  root = selector()
  overflow hidden
  for i in (1..3)
    &:nth-of-type({i})
      {root}__link
        transition-delay: 0.7s;
  &__link
    display inline-block
    padding 10px 0
    color inherit
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
      font-size 3.46666vw
    +pointer-device()
      &:hover
        {root}__account
          opacity 1
  &__account
    opacity opacity
    transition .4s

.contact
  root = selector()
  overflow hidden
  &__wrap
    display inline-block
    opacity 0
    transform translateY(105%) translateZ(0)
    transition .8s cubic-bezier(.165,.84,.44,1) 0.7s
  &__link
    display flex
    align-items center
    padding 10px 0
    color inherit
    font-family museo-sans
    font-size 1.2rem
    line-height 1
    letter-spacing .04rem
    transition .6s
    +tl()
      font-size 1.5625vw
    +sp()
      font-size 3.2vw
    +pointer-device()
      &:hover
        {root}__icon
          opacity 1
  &__icon
    display inline-block
    width 0.8vw
    height auto
    margin-top -2px
    margin-left 4px
    transition .2s
    opacity 0

.loaded
  // .title__wrap,
  .copy__text,
  .list__link,
  .contact__wrap
    opacity 1 !important
    transform translateZ(0) !important

</style>
