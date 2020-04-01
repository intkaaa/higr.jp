<template lang="pug">
  svg.logo(width="25" height="45" viewbox="0 0 25 45" fill="none" xmlns="http://www.w3.org/2000/svg")
    path(d="M0 45L3.30556 41.9739V17.4564L0 20.4826V45Z" fill="#152040")
    path(d="M7.23016 39.1798L10.5357 36.1537V11.6403L7.23016 14.6624V39.1798Z" fill="#152040")
    path(d="M14.4643 33.3598L17.7699 30.3336V5.82019L14.4643 8.84234V33.3598Z" fill="#152040")
    path(d="M21.6945 3.02615V27.5396L25 24.5134V0L21.6945 3.02615Z" fill="#152040")
</template>

<style lang="stylus" scoped>
.logo
  display inline-block
  path
    fill base
    [data-mode="dark"] &
      fill dark_accent
</style>
