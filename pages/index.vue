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

        label.content__toggle.toggle
          input#js-toggle.toggle__switch(type="checkbox")
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

    // Toggle
    if (window.matchMedia('(prefers-color-scheme: dark)').matches) {
      document.documentElement.setAttribute('data-mode', 'dark')
    } else if (window.matchMedia('(prefers-color-scheme: light)').matches) {
      document.documentElement.setAttribute('data-mode', 'light')
    }
    const checkToggle = document.getElementById('js-toggle')
    let mode = document.documentElement.getAttribute('data-mode')
    console.log(mode)
    checkToggle.addEventListener('change', function(e) {
      if (mode === 'dark') {
        document.documentElement.setAttribute('data-mode', 'light')
        mode = 'light'
        console.log(mode)
      } else {
        document.documentElement.setAttribute('data-mode', 'dark')
        mode = 'dark'
        console.log(mode)
      }
    })
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
    position fixed
    top -100%
    left -50%
    width 300%
    height 300%
    opacity 0.3
    background-image url('/noise.png')
    animation grain 8s steps(10) infinite
    [data-mode="dark"] &
      opacity 0.03
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

.toggle
  width 24px
  height 24px
  border 2px solid
  border-color inherit
  border-radius 12px
  cursor pointer
  &__switch
    display none

.loaded
  // .title__wrap,
  .copy__text,
  .list__link,
  .contact__wrap
    opacity 1 !important
    transform translateZ(0) !important

</style>
