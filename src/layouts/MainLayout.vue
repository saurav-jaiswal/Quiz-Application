<template>
  <q-layout view="hHh LpR fFf" class="bg-grey-3">
    <q-header class="bg-grey-3 text-grey-9" reveal height-hint="60">
      <q-toolbar class="GPLAY__toolbar text-grey-6">
        <q-btn
          v-if="this.$q.platform.is.mobile || !leftDrawerOpen"
          flat
          dense
          round
          @click="leftDrawerOpen = !leftDrawerOpen"
          aria-label="Menu"
          icon="menu"
          class="q-mr-sm"
        />

        <div class="q-pr-lg">
          <h4>Quiz App</h4>
        </div>

      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      content-class="bg-grey-3 text-grey-7"
      :width="200"
    >
      <q-list>

        <q-item clickable class="GPLAY__drawer-link bg-grey-10 text-grey-3">
          <q-item-section avatar class="text-grey-1">
            <q-icon name="weekend" />
          </q-item-section>
          <q-item-section class="text-grey-3">
            <q-item-label>Menu</q-item-label>
          </q-item-section>
        </q-item>

        <q-item clickable class="GPLAY__drawer-link GPLAY__drawer-link--apps" to="/">
          <q-item-section avatar class="bg-grey-7 text-grey-1 text-center">
            <q-icon name="home" />
          </q-item-section>
          <q-item-section class="apps-text" >
            <q-item-label>Home</q-item-label>
          </q-item-section>
        </q-item>


        <q-item clickable class="GPLAY__drawer-link GPLAY__drawer-link--apps" to="/computer_quiz">
          <q-item-section avatar class="bg-green-7 text-grey-1 text-center">
            <q-icon name="computer" />
          </q-item-section>
          <q-item-section class="apps-text" >
            <q-item-label>Computer</q-item-label>
          </q-item-section>
        </q-item>

        <q-item clickable class="GPLAY__drawer-link GPLAY__drawer-link--movies" to="current_affairs">
          <q-item-section avatar class="movies-icon bg-red-7 text-grey-1 text-center">
            <q-icon name="psychology" />
          </q-item-section>
          <q-item-section class="movies-text">
            <q-item-label>Current Affairs</q-item-label>
          </q-item-section>
        </q-item>

<!--        <q-item clickable class="GPLAY__drawer-link GPLAY__drawer-link&#45;&#45;music">-->
<!--          <q-item-section avatar class="music-icon bg-orange-7 text-grey-1 text-center">-->
<!--            <q-avatar size="22px" color="white" text-color="orange-7" icon="music_note" />-->
<!--          </q-item-section>-->
<!--          <q-item-section class="music-text">-->
<!--            <q-item-label>Music</q-item-label>-->
<!--          </q-item-section>-->
<!--        </q-item>-->

<!--        <q-item clickable class="GPLAY__drawer-link GPLAY__drawer-link&#45;&#45;books">-->
<!--          <q-item-section avatar class="books-icon bg-blue-7 text-grey-1 text-center">-->
<!--            <q-icon name="book" />-->
<!--          </q-item-section>-->
<!--          <q-item-section class="books-text">-->
<!--            <q-item-label>Books</q-item-label>-->
<!--          </q-item-section>-->
<!--        </q-item>-->

<!--        <q-item clickable class="GPLAY__drawer-link GPLAY__drawer-link&#45;&#45;devices">-->
<!--          <q-item-section avatar class="devices-icon bg-blue-grey-7 text-grey-1 text-center">-->
<!--            <q-icon name="devices" />-->
<!--          </q-item-section>-->
<!--          <q-item-section class="devices-text">-->
<!--            <q-item-label>Devices</q-item-label>-->
<!--          </q-item-section>-->
<!--        </q-item>-->
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />

<!--      <q-page-sticky expand position="top">-->
<!--        <q-toolbar class="GPLAY__sticky bg-white q-px-xl">-->
<!--          <q-space />-->
<!--          <q-btn icon="help" dense flat size="12px" class="GPLAY__sticky-help" />-->
<!--          <q-btn icon="settings" dense flat class="GPLAY__sticky-settings q-ml-md" size="12px" />-->
<!--        </q-toolbar>-->
<!--      </q-page-sticky>-->
    </q-page-container>
  </q-layout>
</template>

<script>
export default {
  name: 'GooglePlayLayout',
  data () {
    return {
      leftDrawerOpen: false,
      search: '',
      storage: 0.26,
      links1: [
        { text: 'Account' },
        { text: 'Payment methods' },
        { text: 'My subscriptions' },
        { text: 'Redeem' },
        { text: 'Buy gift card' },
        { text: 'My wishlist' },
        { text: 'My Play activity' },
        { text: 'Parent guide' }
      ]
    }
  }
}
</script>

<style lang="sass">
.GPLAY
  &__toolbar
    height: 60px
  &__logo
    width: 183px
    height: 39px
  &__toolbar-input-container
    min-width: 100px
    width: 55%
  &__toolbar-input-btn
    border-radius: 0
    max-width: 60px
    width: 100%
  &__drawer-link
    .q-item__section--avatar
      margin: -8px 0 -8px -16px
      padding: 8px 0 8px 16px
    .q-item__section--main
      margin: -8px -16px -8px 16px
      padding: 8px 16px 8px 2px
      font-size: 18px
      font-weight: 300
    &--apps, &--movies, &--music, &--books, &--devices
      background: #f5f5f5!important
      &:hover
        color: #eee !important
    &--apps:hover
      background: #43a047!important
    &--movies:hover
      background: #e53935!important
    &--music:hover
      background: #fb8c00!important
    &--books:hover
      background: #1e88e5!important
    &--devices:hover
      background: #546e7a!important
  &__drawer-item
    padding: 6px 12px 6px 23px
  &__sticky
    min-height: 49px
    border-bottom: 1px solid rgba(0,0,0,0.12)
  &__sticky-help
    border: 1px solid #ccc
    padding-left: 8px
    padding-right: 8px
  &__sticky-settings
    padding-left: 17px
    padding-right: 17px
    border: 1px solid #ccc
</style>
