<template lang="pug">
  .container
    main.main
      .content
        h1.content__title.title
          a.title__wrap(href="/", aria-label="Higher")
            Logo.js-loaded-fade

        .content__read.read
          p.read__copy.copy
            span.copy__row
              span.copy__text.js-loaded-ease Hi. My name is Taka.
            span.copy__row
              span.copy__text.js-loaded-ease I’m a designer and developer
            span.copy__row
              span.copy__text.js-loaded-ease based in Tokyo.

          ul.read__lists.lists
            li.lists__list.list
              a.list__link.js-loaded-ease(href="https://dribbble.com/intkaaa", target="_blank")
                span.list__service dribbble

            li.lists__list.list
              a.list__link.js-loaded-ease(href="https://twitter.com/intkaaa", target="_blank")
                span.list__service twitter

            li.lists__list.list
              a.list__link.js-loaded-ease(href="https://note.mu/intkaaa", target="_blank")
                span.list__service note

        .content__contact.contact
          span.contact__wrap.js-loaded-ease
            a.contact__link(href="https://m.me/intkaaa", target="_blank") Say hi.
              Messenger.contact__icon

        label.content__toggle.toggle.js-loaded-fade
          input#js-toggle.toggle__switch(type="checkbox")
          Dark.toggle__dark
</template>

<script>
import Logo from '~/components/Logo.vue'
import Messenger from '~/components/Messenger.vue'
import Dark from '~/components/Dark.vue'
import anime from 'animejs'

export default {
  components: {
    Logo,
    Messenger,
    Dark
  },

  mounted() {
    this.$nextTick(() => {
      const viewportUnitsBuggyfill = require('viewport-units-buggyfill')
      viewportUnitsBuggyfill.init()
    })

    this.loadedAnimEase()
    this.loadedAnimFade()

    // Toggle
    if (window.matchMedia('(prefers-color-scheme: dark)').matches) {
      document.documentElement.setAttribute('data-mode', 'dark')
    } else if (window.matchMedia('(prefers-color-scheme: light)').matches) {
      document.documentElement.setAttribute('data-mode', 'light')
    }
    const checkToggle = document.getElementById('js-toggle')
    let mode = document.documentElement.getAttribute('data-mode')
    checkToggle.addEventListener('change', function(e) {
      if (mode === 'dark') {
        document.documentElement.setAttribute('data-mode', 'light')
        mode = 'light'
      } else {
        document.documentElement.setAttribute('data-mode', 'dark')
        mode = 'dark'
      }
    })
  },

  methods: {
    loadedAnimEase() {
      anime({
        targets: '.js-loaded-ease',
        translateY: ['105%', 0],
        opacity: [0, 1],
        easing: 'cubicBezier(.165,.84,.44,1)',
        duration: 1200,
        delay: 1000
      })
    },
    loadedAnimFade() {
      anime({
        targets: '.js-loaded-fade',
        opacity: [0, 1],
        easing: 'cubicBezier(.165,.84,.44,1)',
        duration: 1200,
        delay: 100
      })
    }
  }
}
</script>

<style lang="stylus">
html
  transition 0.4s
  @media (prefers-color-scheme: light)
    color base
    border-color base
    background white
  @media (prefers-color-scheme: dark)
    color dark_accent
    border-color dark_accent
    background dark_base
  &[data-mode="light"]
    color base !important
    border-color base !important
    background white !important
  &[data-mode="dark"]
    color dark_accent !important
    border-color dark_accent !important
    background dark_base !important

.container
  position relative
  &::before
    content ''
    z-index -1
    position fixed
    top -100%
    left -50%
    width 300%
    height 300%
    opacity 0.3
    background-image url('/noise.png')
    animation grain 8s steps(10) infinite
    [data-mode="dark"] &
      opacity 0.024
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
    padding 9.3333vw 0
  +sp()
    width 84%
    padding 9.3333vw 0

.content
  display flex
  flex-direction column
  align-items flex-start
  height 100%
  &__toggle
    position absolute
    bottom 80px
    right 10%
    +sp()
      bottom 40px
      right 8%

.title
  overflow hidden
  &__wrap
    display inline-block

.read
  display flex
  flex-direction column
  justify-content center
  flex-grow 1
  width 100%
  &__copy
    margin-top -6%
    +tl()
      margin-top -28%
  &__lists
    margin-top 40px
    +tl()
      margin-top 24px

.copy
  font-family minion-pro-caption
  font-size 6vh
  line-height 128%
  letter-spacing .08rem
  +tl()
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

.lists
  display flex
  &__list
    margin-right 28px

.list
  overflow hidden
  &__link
    display inline-block
    padding 10px 0
    color inherit
    font-family museo-sans
    font-size 2vh
    line-height 1
    letter-spacing .04rem
    opacity 0
    +tl()
      font-size 1.5625vw
    +sp()
      padding 6px 0
      font-size 3.46666vw
  &__service
    display block
  &__account
    opacity opacity

.contact
  root = selector()
  overflow hidden
  &__wrap
    display inline-block
    opacity 0
  &__link
    display flex
    align-items center
    padding 10px 0
    color inherit
    font-family museo-sans
    font-size 1.2rem
    line-height 1
    letter-spacing .04rem
    +tl()
      font-size 1.5625vw
    +sp()
      font-size 3.2vw
    +pointer-device()
      &:hover
        {root}__icon
          opacity 1
  &__icon
    display block
    width 1.2rem
    height 1.2rem
    margin-top -2px
    margin-left 4px
    transition .2s
    opacity 1
    +pointer-device()
      opacity 0

.toggle
  width 24px
  height 24px
  border 2px solid
  border-radius 12px
  cursor pointer
  @media (prefers-color-scheme: light)
    border-color inherit
  [data-mode="light"] &
    border-color inherit
  @media (prefers-color-scheme: dark)
    border-color transparent
  [data-mode="dark"] &
    border-color transparent
  &__switch
    display none
  &__dark
    position absolute
    bottom -2px
    right -2px
    width 24px
    height 24px

</style>
