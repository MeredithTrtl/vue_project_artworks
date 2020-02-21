<template lang="html">
  <main>
    <h1>cool gallery</h1>
    <artwork-detail
    v-if="selectedArtwork"
    :artwork='selectedArtwork'></artwork-detail>
    <artwork-list :artworks='artworks'></artwork-list>
  </main>
</template>

<script>
import { eventBus } from './main.js'
import artworkList from './components/artworkList.vue'
import artworkDetail from './components/artworkDetail.vue'

export default {
  name: 'app',
  data(){
    return{
      artworks: [],
      selectedArtwork: null
    }
  },
  methods:{
    getArtworks: function(){
      return fetch('https://www.rijksmuseum.nl/api/en/collection?key=M9jFGAc3&q=still%life&ps=100&s=relevance&type=painting')
      .then(res => res.json())
      .then(artworks => this.artworks = artworks.artObjects);
    }
  },
  mounted(){
    this.getArtworks();

    eventBus.$on('artwork-selected', artwork => (this.selectedArtwork = artwork))

  },
  components: {
    "artwork-list": artworkList,
    "artwork-detail": artworkDetail
  },
}
</script>

<style lang="css" scoped>
</style>


<!-- fetch('https://api.punkapi.com/v2/beers')
.then(res => res.json())
.then(beers => this.beers = beers) -->
