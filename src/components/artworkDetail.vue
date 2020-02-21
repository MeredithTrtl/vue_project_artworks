<template lang="html">
  <section>
    <p>{{artwork.longTitle}}</p>
      <a :href="artwork['links'].web">Museum Site</a>
  </section>

</template>

<script>
export default {
  name: 'artwork-detail',
  props: ['artwork']
}
</script>

<style lang="css" scoped>

section{
}

</style>
