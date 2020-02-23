<template lang="html">
    <div class="page">
    <div class="header">
      <artwork-header :images='images'></artwork-header>
    </div>
    <div class ='main'>
      <div class="top">
        <h1>The Stillest Lives</h1>
        <my-artworks-list :myArtworks='myArtworks'></my-artworks-list>
        <artwork-detail
        v-if="selectedArtwork"
        :artwork='selectedArtwork'></artwork-detail>
        <artwork-list :artworks='artworks'></artwork-list>
      </div>
    </div>
    </div>

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
      return fetch('https://www.rijksmuseum.nl/api/en/collection?key=M9jFGAc3&q=still%life&ps=100&s=relevance&type=painting')
      .then(res => res.json())

      .then(data => {
        const artworkData = data.artObjects
        artworkData.forEach(artwork => (artwork.inMyGallery = false));
        this.artworks = artworkData;
      })
    },

    getImages: function(){
      return fetch('https://www.rijksmuseum.nl/api/en/collection?key=M9jFGAc3&q=still%life&ps=100&s=relevance&&type=painting')
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

.page {
  background-color: #1a0d00;
  color: #fff3e6;
  font-family: arial, ;
}

.main {
  display: flex;
}

.header {
  width: 100%;
  height: 460px;
}

</style>


<!--  -->
