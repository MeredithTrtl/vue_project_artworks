<template lang="html">
  <main>
    <h1>cool gallery</h1>
    <my-artworks-list :myArtworks='myArtworks'></my-artworks-list>
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
import myArtworksList from './components/myArtworksList.vue'

export default {
  name: 'app',
  data(){
    return{
      artworks: [],
      selectedArtwork: null
    }
  },
  computed: {
    myArtworks: function(){
      return this.artworks.filter(artwork => artwork.inMyGallery)
    }
  },
  methods:{
    getArtworks: function(){
      return fetch('https://www.rijksmuseum.nl/api/en/collection?key=M9jFGAc3&q=still%life&ps=100&s=relevance&type=painting')
      .then(res => res.json())

      .then(data => {
          const artworkData = data.artObjects
          artworkData.forEach(artwork => (artwork.inMyGallery = false));
          this.artworks = artworkData;
        })

    },
    addToGallery: function(artwork){
      const index = this.artworks.indexOf(artwork);
      this.artworks[index].inMyGallery = true;
    }
  },
  mounted(){
    this.getArtworks();

    eventBus.$on('artwork-selected', artwork => (this.selectedArtwork = artwork))

    eventBus.$on('add-to-gallery', artwork => this.addToGallery(artwork))

  },
  components: {
    "artwork-list": artworkList,
    "artwork-detail": artworkDetail,
    "my-artworks-list": myArtworksList
  },
}
</script>

<style lang="css" scoped>
</style>


<!-- fetch('https://api.punkapi.com/v2/beers')
.then(res => res.json())
.then(beers => this.beers = beers) -->
