<!-- SCRIPT -->
<script>
    export default {

  data() {
    return {
      
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

<div class="row">
    <div class="text_col">
        <h2>BoolFlix</h2>
    </div>
    <div class="utility_col">
        <div class="search_box">
            <input type="text" placeholder="Search...">
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
    width: 150px;
}
</style>
