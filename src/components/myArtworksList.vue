<template lang="html">
  <section v-if='myArtworks.length'>
    <h4>My Gallery</h4>
    <div class="list">
      <my-artworks-list-item v-for="(myArtwork, index) in myArtworks"
      :myArtwork = "myArtwork"
      :key = "index">
    </my-artworks-list-item>
    </div>
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

.list{
  display: flex;

}

</style>
