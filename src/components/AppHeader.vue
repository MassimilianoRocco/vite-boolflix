<!-- SCRIPT -->
<script>
    import axios from 'axios';
    import store from '../data/store.js';

    export default {

  data() {
    return {
        userSearch:"",

        store,
    }
  },
  methods: {

    // GETALLMOVIES ON CREATED
    getAllMovies(){
        const options = {
        method: 'GET',
        url: 'https://api.themoviedb.org/3/movie/popular',
        params: {include_adult: 'true', language: 'en-US', page: '1'},
        headers: {
            accept: 'application/json',
            Authorization: 'Bearer eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiI3MzE5MmFlYjcyZDY5NDI1MGFkYzYxODJhOTk1NmVjMyIsInN1YiI6IjY2NTcwYWQ1ZmVlNjZlZmZiNWU0ZTUxNSIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.pOvQ1OKAYU2WHehpISSAFEQetdRMxLF2-h2lW5U6Szo'
        }
        };

        axios
        .request(options)
        .then((response)=> {
            console.log(response.data);
            this.store.Movies = response.data.results;
            console.log(this.store)  //Con l'arrow function e i "this." errori vari
        })
        .catch(function (error) {
            console.error(error);
        });
    },

    // GETMOVIES ON SEARCH
    getMovies(){
        
        if(this.userSearch){
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
            .then((response)=> {
                console.log(response.data);
                this.store.Movies = response.data.results;
            })
            .catch(function (error) {
                console.error(error);
            });
        }
        else{
            this.getAllMovies();
        }
    },

    // GETALLSERIES ON TV SERIES h4 CLICK
    getAllTvSeries(){
        const options = {
            method: 'GET',
            url: 'https://api.themoviedb.org/3/tv/popular',
            params: {language: 'en-US', page: '1'},
            headers: {
                accept: 'application/json',
                Authorization: 'Bearer eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiI3MzE5MmFlYjcyZDY5NDI1MGFkYzYxODJhOTk1NmVjMyIsInN1YiI6IjY2NTcwYWQ1ZmVlNjZlZmZiNWU0ZTUxNSIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.pOvQ1OKAYU2WHehpISSAFEQetdRMxLF2-h2lW5U6Szo'
            }
            };

            axios
            .request(options)
            .then((response)=> {
                console.log(response.data);
                this.store.Series = response.data.results;
            })
            .catch(function (error) {
                console.error(error);
            });
    },


     // GETSERIES ON SEARCH
    getTvSeries(){
        const options = {
            method: 'GET',
            url: 'https://api.themoviedb.org/3/search/tv',
            params: {query: this.userSearch, include_adult: 'true', language: 'en-US', page: '1'},
            headers: {
                accept: 'application/json',
                Authorization: 'Bearer eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiI3MzE5MmFlYjcyZDY5NDI1MGFkYzYxODJhOTk1NmVjMyIsInN1YiI6IjY2NTcwYWQ1ZmVlNjZlZmZiNWU0ZTUxNSIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.pOvQ1OKAYU2WHehpISSAFEQetdRMxLF2-h2lW5U6Szo'
            }
            };

        axios
        .request(options)
        .then((response)=> {
            console.log(response.data);
            this.store.Series = response.data.results;
        })
        .catch(function (error) {
            console.error(error);
        });
    },




    setStoreIsMovie(){
        store.isMovie = true;
    },
    setStoreIsSeries(){
        store.isMovie = false;
    }

  },
  created() {
    this.getAllMovies()
},
mounted() {
    
  }
}
</script>

<!-- TEMPLATE -->
<template> 

<div class="row">
    <div class="text_col">
        <h1>BoolFlix</h1>
        <h4 @click="setStoreIsMovie(), getAllMovies()">Movies</h4>
        <h4 @click="setStoreIsSeries(), getAllTvSeries()">Tv Series</h4>
    </div>
    <div class="utility_col">
        <div class="search_box">
            <input v-if="store.isMovie==true" type="text" v-model="userSearch" @keyup.enter="getMovies()" placeholder="Search...">
            <input v-else type="text" v-model="userSearch" @keyup.enter="getTvSeries()" placeholder="Search...">
        </div>
    </div>
</div>
    
</template>

<!-- STYLE -->
<style scoped>
.row{
    width: 100%;
    height: 100px;
    padding: 0 1rem;
    background-color: #2e2d2d;
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.text_col{
    width: 50%;
    display: flex;
    align-items: center;
}
.text_col>h1{
    margin-right: 4rem;
    color: #E50914;
}
.text_col h4{
    margin: 0 1rem;
    cursor: pointer;
    color: white;
}

.utility_col{
    width: 50%;
    color: white;
    display: flex;
    justify-content: flex-end;
}

.search_box input{
    border-radius: 10px;
    padding: 0.5rem;
    margin-right: 1rem;
    width: 150px;
}
input[type=text]:focus {
  width: 300px;
  transition: width 0.4s ease-in-out;
}
</style>
