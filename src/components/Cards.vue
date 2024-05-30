<!-- SCRIPT -->
<script>
    import store from '../data/store.js';

    export default {
      name: "Cards",
      props: {
        singleMovie: Object,
      },
  data() {
    return {
      standardUrl: 'https://image.tmdb.org/t/p/w185',
      store,
    }
  },

  methods: { 

        // GETIMAGE FUNCTION
        getImage(){
          let url;
          if(this.singleMovie.poster_path){
          url = this.standardUrl + this.singleMovie.poster_path;
          }
          else{
            url = "https://picsum.photos/200/300";
          }
          return url
        },

        // VOTE FUNCTION
        getFixedVote(){
          let num;
          let roundedNum;
          if(this.singleMovie.vote_average){
            num = this.singleMovie.vote_average / 2;
            roundedNum = Math.round(num * 10) / 10

            return roundedNum;
          }
          else{
            return "Not enough votes";
          }
        }
  },
  created() {
   
  },
  mounted() {

  }
}

</script>

<!-- TEMPLATE -->
<template>
    <div class="card">
      <div class="movie_info_box">
      <img v-if="store.isMovie==true" :src="getImage()"  alt="movie img">
      <img v-else :src="getImage()"  alt="movie img">

        <p v-if="store.isMovie==true">Title: {{singleMovie.title ?  singleMovie.title : 'No Name'}}</p>
        <p v-else>Title: {{singleMovie.name ?  singleMovie.name : 'No Name'}}</p>

        <p v-if="store.isMovie==true">Original Title: {{singleMovie.original_title ?  singleMovie.original_title : 'No Name'}}</p>
        <p v-else>Original Name: {{singleMovie.original_name ?  singleMovie.original_name : 'No Name'}}</p>


        <p v-if="store.isMovie==true">Language: {{singleMovie.original_language ?  singleMovie.original_language : 'No Lang'}}</p>
        <p v-else>Language: {{singleMovie.original_language ?  singleMovie.original_language : 'No Lang'}}</p>


        <p v-if="store.isMovie==true"><i class="fa-solid fa-star" style="color: #FFD43B;"></i> {{getFixedVote()}}</p>
        <p v-else>
          <i class="fa-solid fa-star" style="color: #FFD43B;"></i>
           {{getFixedVote()}}
        </p>
      </div>
    </div>
</template>

<!-- STYLE -->
<style scoped>
     .card{
        width: calc((100% / 6));
        text-align: center;
        padding: 1rem;
    }
    .card img{
        width: 100%;
        height: 80%;
        object-fit: cover;
    }
    .movie_info_box{
      background-color:  #2e2d2d;
      color: white;
      height: 500px;
      overflow: auto;
    }
    .movie_info_box p{
      margin: 4px 0;
      font-size: 0.8rem;
    }
</style>