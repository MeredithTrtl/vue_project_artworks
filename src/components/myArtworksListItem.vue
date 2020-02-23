<template lang="html">
  <section>
    <img :src="myArtwork.webImage.url" alt="">
    <p><button v-on:click="rmvFromGallery">Remove From My Gallery</button></p>
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

section{
  display: flex;
  flex-direction: column;
  padding: 5px;
  align-items: center;
}

img {
  height: 400px;
}
</style>
