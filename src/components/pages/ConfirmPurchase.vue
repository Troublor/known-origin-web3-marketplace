<template>

  <div class="text-center text-blue" v-if="!edition">
    <img src="../../../static/Timer.svg" style="width: 100px"/><br/>
    <span class="loading">Loading...</span>
  </div>

  <div v-else-if="edition">
    <router-link :to="{ name: 'gallery' }" class="back-arrow" style="float: left">
      <img src="../../../static/back_arrow.svg" style="width: 35px"/>
    </router-link>

    <h1>{{ edition.otherMeta.artworkName }}</h1>

    <div class="assets_to_buy">
        <gallery-edition :edition="edition" :purchase="true"></gallery-edition>
    </div>
  </div>
</template>

<script>
  import { mapGetters, mapState } from 'vuex';
  import Artist from '../Artist';
  import GalleryEdition from '../GalleryEdition';
  import ConfirmPurchaseButton from '../ui-controls/ConfirmPurchaseButton';
  import _ from 'lodash';
  import EditionQrCode from '../ui-controls/EditionQrCode';

  export default {
    name: 'confirmPurchase',
    components: {EditionQrCode, GalleryEdition, ConfirmPurchaseButton},
    computed: {
      ...mapGetters([
        'firstAssetForEdition'
      ]),
      edition: function () {
        return this.firstAssetForEdition(this.$route.params.edition);
      },
      title: function () {
        return `${this.edition.editionName} #${this.edition.edition}`;
      },
    },
    methods: {
      countPurchased: (assets) => {
        return _.filter(assets, (val) => {
          return val.purchased === 1 || val.purchased === 2;
        });
      },
      countAvailable: (assets) => {
        return _.filter(assets, {'purchased': 0});
      },
    }
  };
</script>

<style scoped>

</style>
