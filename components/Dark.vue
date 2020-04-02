<template lang="pug">
  svg.dark(xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24")
    path(d="M14.12,2.24A10,10,0,1,1,2.36,14.65a11.42,11.42,0,0,0,3.25.48A9.14,9.14,0,0,0,12,12.7c2.65-2.51,3.45-6.53,2.16-10.46M12,0a10.93,10.93,0,0,0-1.15.06A10.85,10.85,0,0,1,11.9,2c1.42,3.36,1,7-1.32,9.24a7.07,7.07,0,0,1-5,1.88A9.8,9.8,0,0,1,2,12.42a11.07,11.07,0,0,1-2-1c0,.2,0,.4,0,.61a11.59,11.59,0,0,0,.08,1.33A12,12,0,1,0,12.76,0c-.25,0-.5,0-.76,0Z")
</template>

<style lang="stylus" scoped>
.dark
  display inline-block
  path
    fill transparent
    [data-mode="dark"] &
      fill dark_accent
</style>
