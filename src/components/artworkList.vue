<template lang="html">
  <section v-if='artworks.length'>
    <h2>All The Arts</h2>
    <div class="art-list">
    <artwork-list-item
    v-for="(artwork, index) in artworks"
    :artwork = "artwork"
    :key = "index" >
  </artwork-list-item>
  </div>
</section>
</template>

<script>
import artworkListItem from './artworkListItem.vue'

export default {
  name: 'artwork-list',
  props: ['artworks'],
  components: {
    "artwork-list-item": artworkListItem
  }
}
</script>

<style lang="css" scoped>

.art-list{
  width: 60%;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}
</style>
