<template lang="html">
  <section>
    <p>{{myArtwork.longTitle}}</p>
    <img :src="myArtwork.webImage.url" alt="">
  </section>
</template>

<script>
export default {
    name: 'my-artwork-list-item',
    props: ['myArtwork'],
}
</script>

<style lang="css" scoped>

img {
  height: 400px;
}
</style>
