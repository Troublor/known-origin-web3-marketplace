<template>
  <div id="artists">
    <router-link :to="{ name: 'dashboard' }" class="back-arrow" style="float: left">
      <img src="../../../static/back_arrow.svg" style="width: 35px"/>
    </router-link>

    <h1>Artists</h1>

    <div>
      <section class="cards">
        <artist v-for="artist in visibleAssets()" :key="artist.name" :artist="artist"></artist>
      </section>
    </div>

  </div>
</template>

<script>
  import {mapGetters, mapState} from 'vuex';
  import Artist from '../Artist';

  export default {
    name: 'artists',
    components: {Artist},
    computed: {
      ...mapGetters([
        'visibleAssets',
      ]),
      ...mapState([
        'assets',
      ]),
    },
    mounted() {

    },
  };
</script>

<style scoped>

</style>
