<template>
  <div class="antialiased">
    <navigation-main></navigation-main>
    <main>
      <nuxt/>
    </main>
    <modal :show="showNewTalkModal" @close="showNewTalkModal = false">
      <div slot="header">Submit new talk</div>
    </modal>
    <svg-symbols />
  </div>
</template>

<script>

import Modal from "@/components/Modal"
import NavigationMain from "@/components/NavigationMain"
import SvgSymbols from "@/components/SvgSymbols"
import ButtonDefault from '@/components/ButtonDefault'

export default {
  components: { Modal, SvgSymbols, NavigationMain, ButtonDefault },
  data() {
    return {
      showNewTalkModal: false
    }
  },
  methods: {
    openModal() {
      this.showNewTalkModal = true
    }
  }
}
</script>
