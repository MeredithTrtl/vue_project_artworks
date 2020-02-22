<template lang="html">
<section>
  <img v-for="(image, index) in images"
  :image = "image"
  :key = "index"
  :src="image" class="mySlides">
</section>
</template>

<script>
export default {
  name: 'header-image',
  props: ['images']
  }

</script>

<style lang="css" scoped>

</style>
