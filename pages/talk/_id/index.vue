<template>
  <div class="bg-indigo-darkest">
    <loader v-if="$apollo.loading" />
    <section v-else>
      <header class="pattern bg-purple-dark py-24">
        <div class="container mx-auto p-2">
          <h1 class="text-shadow max-w-xl mx-auto text-center p-8 text-center leading-tight text-2xl md:text-5xl text-base text-white font-display font-bold tracking-wide " v-if="talk.name">{{talk.name}}</h1>

          <ul class="flex justify-center list-reset">
            <li class="text-center" v-for="speaker in talk.speakers" :key="speaker.id">
              <nuxt-link :to="`/speaker/${speaker.id}`" class="no-underline">
                <img class="border-2 border-white shadow rounded-full inline-block w-32 h-32" v-if="speaker" :src="speaker.speakerPicture.url" :alt="speaker.name">
                <h2 class="text-shadow py-4 text-center text-white text-xl" v-if="speaker.name">{{speaker.name}}</h2>
              </nuxt-link>
            </li>
          </ul>

        </div>
      </header>
      <div class="max-w-xl mx-auto">
        <div class="md:flex items-center relative">
          <div class="md:w-full p-4 owl">
            <div v-if="talk.youtubecode" class="relative rounded-lg overflow-hidden shadow-lg" style="width: 100%; padding-top: calc(100% * 9 / 16 )">
              <iframe class="absolute pin w-full h-full" type="text/html" :src="`https://www.youtube.com/embed/${talk.youtubecode}`" frameborder="0" />
            </div>
          </div>
        </div>
      </div>
      <div class="mx-auto max-w-xl p-4">
        <div class="font-sans text-xl  leading-normal text-white text-xl font-light" v-html="talk.abstract"></div>
      </div>
    </section>
  </div>
</template>

<script>

import QueryTalk from '~/apollo/queries/talk'

export default {
  apollo: {
    talk: {
      query: QueryTalk,
      prefetch: ({route: {params: {id}}}) => ({ id }),
      variables () {
        return {
          id: this.$route.params.id
        }
      }
    }
  },
  data: () => ({
    talk: '',
  }),
  head() {
    return {
      title: this.talk.name,
      meta: [
        { hid: 'description', name: 'description', content: this.talk.abstract },
        { hid: 'twitter:card', name: "twitter:card", content: "summary_large_image"},
        { hid: 'twitter:site', name: "twitter:site", content: "@webzuerich"},
        { hid: 'twitter:creator', name: "twitter:creator", content: "@aleksejdix"},
        { hid: 'twitter:url', name: "twitter:url", content: process.env.baseUrl + this.$route.path },
        { hid: 'twitter:title', name: "twitter:title", content: this.talk.name},
        { hid: 'twitter:description', name: "twitter:description", content: this.talk.abstract},
        { hid: 'twitter:image', name: "twitter:image", content: `https://us-central1-webzuerich-talk-image-gen.cloudfunctions.net/generateImage?id=xYXhOJZttRpkqxERH8MD&name=${this.talk.speakers && this.talk.speakers[0].name}&title=${this.talk.name}&userImg=${this.talk && this.talk.speakers[0].speakerPicture.url}`},
      ],
      __dangerouslyDisableSanitizersByTagID: { 'twitter:image': ['content'] }
    }
  }
}
</script>
