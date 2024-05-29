<!-- SCRIPT -->
<script>
    export default {
      name: "Cards",
      props: {
        singleMovie: Object,
      },
  data() {
    return {
      standardUrl: 'https://api.themoviedb.org/3/search/movie',
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
    <div class="card">
        <!-- <img :src="singleMovie.poster_path"> -->
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
</style>