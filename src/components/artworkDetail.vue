<template lang="html">
  <section>
    <p>Title: {{artwork.title}}</p>
    <p>Made By: {{artwork.principalOrFirstMaker}}</p>
    <p>Year: {{artwork.longTitle | getDate}}</p>
    <a :href="artwork['links'].web">Museum</a>
  </section>

</template>

<script>
export default {
  name: 'artwork-detail',
  props: ['artwork'],
  filters: {
    getDate(string){
      const array = string.split(' ')
      return array.slice(-1)[0]
    }
  }
}
</script>

<style lang="css" scoped>

section{
}

</style>
