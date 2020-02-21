<template lang="html">
  <main>
    <h1>cool gallery</h1>
    <artwork-list :artworks='artworks'></artwork-list>
  </main>
</template>

<script>
import artworkList from './components/artworkList'

export default {
  name: 'app',
  data(){
    return{
      artworks: []
    }
  },
  methods:{
    getArtworks: function(){
      return fetch('https://www.rijksmuseum.nl/api/en/collection?key=M9jFGAc3&q=still%life&ps=100&s=relevance')
      .then(res => res.json())
      .then(artworks => this.artworks = artworks.artObjects)
    }
  },
  mounted(){
    this.getArtworks();
  },
  components: {
    "artwork-list": artworkList
  },
}
</script>

<style lang="css" scoped>
</style>


<!-- fetch('https://api.punkapi.com/v2/beers')
.then(res => res.json())
.then(beers => this.beers = beers) -->
