<!-- SCRIPT -->
<script>
    export default {
      name: "Cards",
      props: {
        singleMovie: Object,
      },
  data() {
    return {
      standardUrl: 'https://image.tmdb.org/t/p/w185',
    }
  },
  methods: { 
        getImage(){
            let url = this.standardUrl + this.singleMovie.poster_path;
            return url;
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
        <img :src="getImage()" alt="movie img">
        <p>{{singleMovie.original_title ?  singleMovie.original_title : 'No Name'}}</p>
    </div>
</template>

<!-- STYLE -->
<style scoped>
     .card{
        width: calc(100% / 6);
        margin-top: 0.5rem;
        text-align: center;
    }
    .card img{
        width: 100%;
        height: 80%;
        object-fit: cover;
    }
</style>