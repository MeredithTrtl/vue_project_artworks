<template lang="html">
  <section>
    <p>{{myArtwork.longTitle}}</p>
    <img :src="myArtwork.webImage.url" alt="">
    <p><button v-on:click="rmvFromGallery">Remove From Gallery</button></p>
  </section>
</template>

<script>
import {eventBus} from '../main.js'

export default {
    name: 'my-artwork-list-item',
    props: ['myArtwork'],
    methods: {
      rmvFromGallery: function(){
        eventBus.$emit("rmv-from-gallery", this.myArtwork)
      }
    }
}
</script>

<style lang="css" scoped>

img {
  height: 400px;
}
</style>
