<!-- SCRIPT -->
<script>
import store from '../data/store.js';
import Cards from './Cards.vue';

import axios from 'axios';

    export default {
        components: {
            Cards,
    },

  data() {
    return {
      store,
      userSearch:"",
    }
  },
  methods: {
    getMovies(){
        
        const options = {
        method: 'GET',
        url: 'https://api.themoviedb.org/3/search/movie',
        params: {query: this.userSearch, include_adult: 'true', language: 'en-US', page: '1'},
        headers: {
            accept: 'application/json',
            Authorization: 'Bearer eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiI3MzE5MmFlYjcyZDY5NDI1MGFkYzYxODJhOTk1NmVjMyIsInN1YiI6IjY2NTcwYWQ1ZmVlNjZlZmZiNWU0ZTUxNSIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.pOvQ1OKAYU2WHehpISSAFEQetdRMxLF2-h2lW5U6Szo'
        }
        };

        axios
        .request(options)
        .then(function (response) {
            console.log(response.data);
            store.Movies = response.data.results;
            console.log(store)  //Con l'arrow function e i "this." errori vari
        })
        .catch(function (error) {
            console.error(error);
        });

    }
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

        <div class="utility_col">
            <div class="search_box">
                <input type="text" v-model="userSearch" @keyup.enter="getMovies()" placeholder="Search...">
            </div>
        </div>


        <div class="card_col">
            <div v-for="card in store.Movies" class="card">{{ card.original_title }}</div>
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
    }
    .card{
        width: calc(100% / 6);
        margin-top: 0.5rem;
        text-align: center;
    }
</style>
