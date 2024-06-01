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
      lang: {
        "en": "https://upload.wikimedia.org/wikipedia/en/a/ae/Flag_of_the_United_Kingdom.svg",
        "it": "https://upload.wikimedia.org/wikipedia/commons/0/03/Flag_of_Italy.svg",
        "fr": "https://upload.wikimedia.org/wikipedia/commons/c/c3/Flag_of_France.svg",
      },
      flagChecked:true,

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
            roundedNum = Math.round(num * 10) / 10;

            return roundedNum;
          }
          else{
            return "Not enough votes";
          }
        },

        getFlag(){
          if((Object.keys(this.lang)).includes(this.singleMovie.original_language)){
            this.flagChecked = true;
            return this.lang[this.singleMovie.original_language];
          }
          else{
            this.flagChecked = false;
          }
        },
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

      <!-- IMG 1:MOVIE  2:TV SERIES -->
      <div class="movie_info_box">
        <img v-if="store.isMovie==true" :src="getImage()"  alt="movie img" class="back_img">
        <img v-else :src="getImage()"  alt="movie img" class="back_img">

        <div class="text_box">

            <!-- Title   1:MOVIE  2:TV SERIES-->
            <p v-if="store.isMovie==true"><b>Title: </b> <span class="text_from_data">{{singleMovie.title ?  singleMovie.title : 'No Name'}}</span></p>
            <p v-else> <b>Title:</b> <span class="text_from_data">{{singleMovie.name ?  singleMovie.name : 'No Name'}}</span></p>

            <!-- Original Title -->
            <p v-if="store.isMovie==true"><b>Original Title: </b><span class="text_from_data">{{singleMovie.original_title ?  singleMovie.original_title : 'No Name'}}</span></p>
            <p v-else><b>Original Name: </b><span class="text_from_data">{{singleMovie.original_name ?  singleMovie.original_name : 'No Name'}}</span></p>

            <!-- Description -->
            <p v-if="store.isMovie==true"><b>Description: </b><br><span class="text_from_data">{{singleMovie.overview ?  singleMovie.overview : 'No Description'}}</span></p>
            <p v-else><b>Description: </b><br><span class="text_from_data">{{singleMovie.overview ?  singleMovie.overview : 'No Description'}}</span></p>

            <!-- Lang -->
            <p v-if="store.isMovie==true" class="flag_box">
              <b>Language: </b>
              <img v-show="this.flagChecked==true" class="flag" :src="getFlag()" alt="flag">
              <span v-show="this.flagChecked==false">{{ this.singleMovie.original_language }}</span>
            </p>
            <p v-else class="flag_box">
              <b>Language: </b>
              <img v-show="this.flagChecked==true" class="flag" :src="getFlag()" alt="flag">
              <span v-show="this.flagChecked==false">{{ this.singleMovie.original_language }}</span>
            </p>

            <!-- Rating -->
            <p v-if="store.isMovie==true"> <b>Rating: </b>
              <span v-for="elemento in 5">
                <span v-show="getFixedVote()>=elemento"><i class="fa-solid fa-star" style="color: #FFD43B;"></i></span>
              </span>
            </p>
            <p v-else>  <b>Rating: </b> 
              <span v-for="elemento in 5">
                <span v-show="getFixedVote()>=elemento"><i class="fa-solid fa-star" style="color: #FFD43B;"></i></span>
              </span>
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
        transition: all 0.5s ease-in-out;
    }
    .card:hover{
      transform: scale(1.1,1.1)
    }
    .card .back_img{
        width: 100%;
        height: 100%;
        display: block;
        object-fit: cover;
    }
    .movie_info_box{
      background-color:  #2e2d2d;
      color: white;
      height: 100%;
    }
    .movie_info_box p{
      max-width: 90%;
      margin: 4px auto;
    }
    .text_box{
      position: absolute;
      width: 100%;
      height: 100%;
      max-height: 90%;
      padding: 1rem;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      opacity: 0;
      overflow: auto;
      font-size: 0.9rem;
    }
    .card:hover .back_img{
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

    .flag_box>.flag{
      width: 25px;
    }


</style>