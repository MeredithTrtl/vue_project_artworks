<template lang="html">
  <main>
    <header>
      <artwork-header :images='images'></artwork-header>
    </header>
    <div class="top">
      <h1>The Stillest Lives</h1>
      <artwork-detail
      v-if="selectedArtwork"
      :artwork='selectedArtwork'></artwork-detail>
      <artwork-list :artworks='artworks'></artwork-list>
    </div>
    <my-artworks-list :myArtworks='myArtworks'></my-artworks-list>
  </main>
</template>

<script>
import { eventBus } from './main.js'
import artworkHeader from './components/artworkHeader.vue'
import artworkList from './components/artworkList.vue'
import artworkDetail from './components/artworkDetail.vue'
import myArtworksList from './components/myArtworksList.vue'

export default {
  name: 'app',
  data(){
    return{
      artworks: [],
      selectedArtwork: null,
      images: []
    }
  },
  computed: {
    myArtworks: function(){
      return this.artworks.filter(artwork => artwork.inMyGallery)
    }
  },
  methods:{
    getArtworks: function(){
      return fetch('https://www.rijksmuseum.nl/api/en/collection?key=M9jFGAc3&q=still%life&ps=100&s=relevance&')
      .then(res => res.json())

      .then(data => {
        const artworkData = data.artObjects
        artworkData.forEach(artwork => (artwork.inMyGallery = false));
        this.artworks = artworkData;
      })
    },

    getImages: function(){
      return fetch('https://www.rijksmuseum.nl/api/en/collection?key=M9jFGAc3&q=still%life&ps=100&s=relevance&')
      .then(res => res.json())

      .then(data => {
        const imageData = data.artObjects;
        let headerImages = []
        imageData.forEach(image => headerImages.push(image.headerImage.url))
        this.images = headerImages;
      })

    },
    addToGallery: function(artwork){
      const index = this.artworks.indexOf(artwork);
      this.artworks[index].inMyGallery = true;
    },
    rmvFromGallery: function(artwork){
      const index = this.artworks.indexOf(artwork);
      this.artworks[index].inMyGallery = false;
    }
  },
  mounted(){
    this.getArtworks();
    this.getImages();

    eventBus.$on('artwork-selected', artwork => (this.selectedArtwork = artwork))

    eventBus.$on('add-to-gallery', artwork => this.addToGallery(artwork))

    eventBus.$on('rmv-from-gallery', artwork => this.rmvFromGallery(artwork))

  },
  components: {
    "artwork-list": artworkList,
    "artwork-detail": artworkDetail,
    "my-artworks-list": myArtworksList,
    "artwork-header": artworkHeader
  },
}
</script>

<style lang="css" scoped>

main {
  display: flex;
}

</style>


<!--  -->
