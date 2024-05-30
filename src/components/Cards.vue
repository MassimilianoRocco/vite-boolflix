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

        <div class="text_box">
            <p v-if="store.isMovie==true"><b>Title: </b> <span class="text_from_data">{{singleMovie.title ?  singleMovie.title : 'No Name'}}</span></p>
            <p v-else> <b>Title:</b> <span class="text_from_data">{{singleMovie.name ?  singleMovie.name : 'No Name'}}</span></p>

            <p v-if="store.isMovie==true"><b>Original Title: </b><span class="text_from_data">{{singleMovie.original_title ?  singleMovie.original_title : 'No Name'}}</span></p>
            <p v-else><b>Original Name: </b><span class="text_from_data">{{singleMovie.original_name ?  singleMovie.original_name : 'No Name'}}</span></p>

            <p v-if="store.isMovie==true"><b>Description: </b><br><span class="text_from_data">{{singleMovie.overview ?  singleMovie.overview : 'No Description'}}</span></p>
            <p v-else><b>Description: </b><br><span class="text_from_data">{{singleMovie.overview ?  singleMovie.overview : 'No Description'}}</span></p>

            <p v-if="store.isMovie==true"><b>Language: </b><span class="text_from_data">{{singleMovie.original_language ?  singleMovie.original_language : 'No Lang'}}</span></p>
            <p v-else><b>Language: </b><span class="text_from_data">{{singleMovie.original_language ?  singleMovie.original_language : 'No Lang'}}</span></p>


            <p v-if="store.isMovie==true"><i class="fa-solid fa-star" style="color: #FFD43B;"></i> {{getFixedVote()}}</p>
            <p v-else>
              <i class="fa-solid fa-star" style="color: #FFD43B;"></i>
              {{getFixedVote()}}
            </p>
        </div>
      </div>
    </div>
</template>

<!-- STYLE -->
<style scoped>
     .card{
        width: calc((100% / 6));
        padding: 1rem;
        position: relative;
        cursor: pointer;
    }
    .card img{
        width: 100%;
        object-fit: cover;
    }
    .movie_info_box{
      background-color:  #2e2d2d;
      color: white;
    }
    .movie_info_box p{
      max-width: 90%;
      margin: 4px auto;
    }
    .text_box{
      position: absolute;
      width: 100%;
      height: 100%;
      padding: 1rem;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      opacity: 0;
      overflow: auto;
    }
    .card:hover img{
      filter: opacity(30%);
      transition: 1s;   
    }
    .card:hover .text_box{
      opacity: 1;
      transition: 1s;
    }

    .text_from_data{
      color: rgb(218, 216, 216);
    }


</style>