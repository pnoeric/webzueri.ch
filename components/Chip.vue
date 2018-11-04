<template>

  <div class="relative">

    <Button v-if="user" @click="open = true">
      {{user.displayName}}
      <img slot="end" class="w-6 h-6 rounded-full mr-2" :src="user.photoURL" :alt="user.displayName">
    </Button>

    <transition slot="dropdown" name="menu" v-if="dropdown">
      <section v-if="user" v-show="open" name="dropdown" class="bg-primary border border-black z-10 shadow absolute rounded-lg  pin-r pin-t w-full" style="min-width: 300px">

        <div class=" px-3 py-4 rounded-t-lg flex">
          <div class="pr-4">
            <img class="rounded-full w-12 h-12 block" :src="user.photoURL" :alt="user.displayName">
          </div>
          <div class="leading-normal flex-1">
            <div class="text-on-dark-primary font-display weight-medium text-base leading-normal">{{user.displayName}}</div>
            <div class="body-2 text-on-dark-secondary">{{user.email}}</div>
          </div>
          <div class="flex items-center self-start">
            <icon-button small @click.stop="open = false"></icon-button>
          </div>
        </div>

        <ul class="list-reset py-2 bg-grey-lighter rounded-b-lg">
          <li class="">
            <nuxt-link class="rounded text-on-light-secondary no-underline transition px-6 flex items-center min-h-12 hover:bg-grey-light  hover:text-on-light-primary" to="/user/">Profile</nuxt-link>
          </li>
          <li class="">
            <a class="rounded text-on-light-secondary no-underline transition px-6 flex items-center min-h-12 hover:bg-grey-light hover:text-on-light-primary" target="_blank" href="https://docs.google.com/forms/u/1/d/e/1FAIpQLSfTaa-_wOFOQv3dZ7Ord9TJ3vN8wNdzUY5VQqzFiTg_WMQwEw/viewform?c=0&w=1">Submit a talk</a>
          </li>
        </ul>

      </section>
    </transition>

  </div>
</template>

<script>
import Button from '~/components/general/Button'
import IconButton from "~/components/icon-button"
import {mapState} from 'vuex'


export default {
  components: {
    IconButton, Button
  },
  computed: {
    ...mapState(['user'])
  },
  data () {
    return {
      dropdown: true,
      open: false
    }
  }
}
</script>
