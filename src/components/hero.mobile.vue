<i18n>
  fr:
    title: UNE {adventure} INCROYABLE DANS UN UNIVERS {unique}
    adventure: AVENTURE
    unique: UNIQUE
    desc: AresRPG est un serveur minecraft sans mods dans lequel votre objectif est de réunir les 6 œufs de dragon. {desc_2}
    desc_2: Le monde est infesté de créatures que vous devrez réduire en poussière pour améliorer votre équipement et vos compétences
    discover: Découvrir
    wip: Le serveur est en développement et proposera un {kick} très prochainement, rejoignez le discord pour être prioritaire !
    email: Enregistrement réussi !
    email_invalid: L'email semble incorrect
  en:
    title: A {adventure} MMORPG EXPERIENCE IN {unique}
    adventure: DELIGHTFUL
    unique: MINECRAFT
    desc: AresRPG is a no mods minecraft mmorpg server in which your goal is to find all 6 dragon eggs. {desc_2}
    desc_2: The world is full of diverse creatures that you can reduce to atoms in order to upgrade your stuff and skills
    discover: Discover
    wip: The server is under construction and will launch a {kick} campaign very soon, join the discord to skip the line !
    email: Sign up sucess !
    email_invalid: Email seems invalid!
</i18n>

<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'
import { useI18n } from 'vue-i18n'

import { fade_up, fade_down } from '../core/anime'

import mail from './mail_input.vue'

const { t } = useI18n()
const scroll_down = () =>
  window.scrollTo({
    top: window.innerHeight,
    behavior: 'smooth',
  })
const twitter = ref()
const telegram = ref()
const discord = ref()
const logo = ref()

const animations = [
  fade_down(logo, 100),
  fade_up(twitter, 200),
  fade_up(telegram, 300),
  fade_up(discord, 600),
]

onMounted(() => {
  animations.forEach(animation => animation.mount())
})
onBeforeUnmount(() => animations.forEach(animation => animation.unmount()))
</script>

<template lang="pug">
.frame
  img.logo(src="../assets/text_logo_fr.png" ref="logo")
  .title
    i18n-t(keypath="title")
      template(#adventure)
        b {{ t('adventure') }}
      template(#unique)
        b {{ t('unique') }}
  .description
    i18n-t(keypath="desc")
      template(#desc_2)
        b {{ t('desc_2')}}
  mail
  a.twitter(href="https://twitter.com/AresRPG" target="_blank" rel="noopener noreferrer" aria-label="Twitter" ref="twitter")
    fa.icon(:icon="['fab', 'twitter']" size="2x")
  a.telegram(href="https://t.me/aresrpg" target="_blank" rel="noopener noreferrer" aria-label="Telegram" ref="telegram")
    fa.icon(:icon="['fab', 'telegram']" size="2x")
  a.discord(href="https://discord.gg/gbkvVJq" target="_blank" rel="noopener noreferrer" aria-label="Discord" ref="discord")
    fa.icon(:icon="['fab', 'discord']" size="2x")
  .wip
    i18n-t(keypath="wip")
      template(#kick)
        b Kickstarter
  .discover(@click="scroll_down")
    span {{t('discover')}}
    img(src="../assets/chevron.svg")
</template>

<style lang="stylus" scoped>
.frame
  display grid
  grid 'logo logo logo' 2fr 'title title title' 1.5fr 'desc desc desc' 2.5fr 'mail mail mail' 1fr 'twitter telegram github' 1fr 'wip wip wip' 1fr 'disc disc disc' 4fr / 1fr 1fr 1fr
  width 100%
  height 100vh
  background url('../assets/mobile_bg_v1.png') bottom / cover
  color #eee
  font-family 'Roboto Condensed'
  place-items center center
  padding 2em
  padding-bottom 1em
  grid-row-gap 1em
  scroll-snap-align start

  .wip
    grid-area wip
    text-transform uppercase
    text-align center
    font-size .7em
    width 100%
    position relative
    text-shadow 1px 2px 5px #212121
    font-weight 900
    z-index 1
    b
      color #09B83E
      text-shadow 1px 2px 5px black
    &::before
      content ''
      position absolute
      width 200vw
      height 150%
      // background crimson
      top -25%
      left -50%
      z-index -1
      backdrop-filter blur(20px)
      // opacity .5
  .logo
    grid-area logo
    object-fit contain
    width 100%
    height 100%
    max-width 400px
  .title
    grid-area title
    text-transform uppercase
    text-align center
    font-size 1.5em
    text-shadow 1px 2px 3px black
    place-self end center
    b
      color #F39C12

  .description
    grid-area desc
    font-size .75em
    text-align center
    font-weight 100
    color #ECF0F1
    display flex
    flex-flow column nowrap
    place-self start center
    b
      margin-top 1em
      font-weight @font-weight

  a
    color white
    display flex
    align-items baseline
    .icon
      filter drop-shadow(1px 2px 3px black)
  .twitter
    grid-area twitter
  .telegram
    grid-area telegram
  .github
    grid-area github
  .discover
    grid-area disc
    display flex
    flex-flow column
    place-self end center
    font-size .9em
    text-shadow 1px 2px 2px black
    animation bounce 7s ease-in infinite
    img
      height 10px

@keyframes bounce
  from, 20%, 53%, 80%, to
    animation-timing-function cubic-bezier(.215, .61, .355, 1)
    transform translate3d(0, 0, 0)
  40%, 43%
    animation-timing-function cubic-bezier(.755, .05, .855, .06)
    transform translate3d(0, -30px, 0)
  70%
    animation-timing-function cubic-bezier(.755, .05, .855, .06)
    transform translate3d(0, -15px, 0)
  90%
    transform translate3d(0, -4px, 0)
</style>
