<template lang="html">
  <section v-if='myArtworks.length'>
    <h4>My Gallery</h4>
    <!-- <p>{{myArtworks}}</p> -->
    <my-artworks-list-item v-for="(myArtwork, index) in myArtworks"
    :myArtwork = "myArtwork"
    :key = "index">
  </my-artworks-list-item>

  </section>
</template>

<script>
import myArtworksListItem from './myArtworksListItem.vue'

export default {
  name: 'my-artworks-list',
  props: ['myArtworks'],
  components: {
    "my-artworks-list-item": myArtworksListItem
  }
}
</script>

<style lang="css" scoped>
</style>
