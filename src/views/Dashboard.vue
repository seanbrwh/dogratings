<template>
  <v-layout>
    <v-flex column justify-center align-center class="text-xs-center" mt-3>
      <h2>User DashBoard</h2>
      <v-card v-for="(rate,idx) in ratedDogs" :key="idx"  style="margin:5vh 2vh">
        <v-layout column justify-center align-center>
            <img :src="rate.dog" alt="" width="300px" style="margin:10px 0">
          <div>
            <h2>
              Notes
            </h2>
            <p>{{rate.Note}}</p>
          </div>
          <div my-2 py-2>
            <h2>
              Rating
            </h2>
            <p>            
              {{rate.rating}}
            </p>
          </div>
        </v-layout>    
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
export default {
  data(){
    return{
      ratedDogs:[]
    }
  },
  mounted(){
    this.ratedDogs = JSON.parse(localStorage.getItem('dogRating'))
  }
}
</script>

<style>
  img{
    display: block;
    max-width: 70vw;
    max-height: 70vw;
    width: auto;
    height: auto;
  }
</style>
