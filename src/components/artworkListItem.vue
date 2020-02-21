<template lang="html">
  <section>
    <p>{{artwork["title"]}} : {{artwork["principalOrFirstMaker"]}}</p>
    <img :src="artwork['webImage'].url" alt="">
  </section>

</template>

<script>
export default {
  name: 'artwork-list-item',
  props: ['artwork']
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

</style>
