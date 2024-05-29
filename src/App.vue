<!-- SCRIPT -->
<script>
import AppHeader from './components/AppHeader.vue'
import AppMain from './components/AppMain.vue'
import store from './data/store.js'

import axios from 'axios';

export default {
  components: {
    AppHeader,
    AppMain,

  },
  data() {
    return {
      store,
      
    }
  },
  methods: {
   
  },
  created() {
    
  },
  mounted() {

  }
}
</script>


<!-- TEMPLATE -->
<template>
  <AppHeader/>
  <AppMain/>

</template>


<!-- STYLE -->
<style scoped>

</style>
