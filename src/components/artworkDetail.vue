<template lang="html">
  <section>
    <p>Now Viewing</p>
    <p>Title: {{artwork.title}}</p>
    <p>Made By: {{artwork.principalOrFirstMaker}}</p>
    <p>Year: {{artwork.longTitle | getDate}}</p>
    <p><a :href="artwork.links.web">Museum</a></p>
    <img :src="artwork.webImage.url" alt="">
    <p><button v-on:click="addToGallery">Add To My Gallery</button></p>
  </section>

</template>

<script>
import {eventBus} from '../main.js'
export default {
  name: 'artwork-detail',
  props: ['artwork'],
  filters: {
    getDate(string){
      const array = string.split(' ')
      return array.slice(-1)[0]
    }
  },
  methods: {
    addToGallery: function(){
      eventBus.$emit("add-to-gallery", this.artwork)
    }
  }
}
</script>

<style lang="css" scoped>

img{
  height: 500px;
}

</style>
