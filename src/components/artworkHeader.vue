<template lang="html">
      <img :src="randomImg" />
</template>

<script>
export default {
  name: 'header-image',
  props: ['images'],

  computed: {
    randomImg: function(){
      return this.images[Math.floor( Math.random() * this.images.length )]
    }
  }
};
</script>

<style lang="css" scoped>


img {
  height:400px;
  width:100%
}

</style>
