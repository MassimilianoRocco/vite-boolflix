<!-- SCRIPT -->
<script>
import store from '../data/store.js';
import Cards from './Cards.vue';

    export default {
        components: {
            Cards,
    },

  data() {
    return {
      store,
    }
  },
  methods: {
   
  },
  computed: {
   
  },
  created() {
   
  },
  mounted() {
  }
}

</script>


<!-- TEMPLATE -->
<template>
    <div class="row">

        <div class="card_col">
            <Cards v-if="store.isMovie==true" v-for="card in store.Movies" :singleMovie="card"/>
            <Cards v-else v-for="card in store.Series" :singleMovie="card"/>
        </div>
    </div>
    
</template>


<!-- STYLE -->
<style scoped>
    .row{
        width: 100%;
        height: calc(100vh - 100px);
        padding: 0 1rem;
        background-color: darkgray;
    }
    .card_col{
        width: 100%;
        height: 100%;
        padding: 2rem 0;
        display: flex;
        flex-wrap: wrap;
        justify-content: flex-start;
        overflow: auto;
    }
</style>
