<template lang="html">
  <section>
    <p>{{artwork["title"]}}</p>
    <img :src="artwork['webImage'].url" alt="">
    <button v-on:click="moreInfo">More Info</button>
  </section>

</template>

<script>
import { eventBus } from '../main.js'

export default {
  name: 'artwork-list-item',
  props: ['artwork'],
  methods: {
    moreInfo: function(){
      eventBus.$emit("artwork-selected", this.artwork)
    }
  }
}
</script>

<style lang="css" scoped>

section{
  display: flex;
  flex-direction: column;
  padding: 20px;
  align-items: center;
}

img {
  height: 300px;
}

button {
  margin-top: 10px;
}

</style>
