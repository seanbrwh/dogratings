<template>
  <v-layout>
    <v-flex column justify-center align-center class="text-xs-center" mt-3>
      <h2>User DashBoard</h2>
      <v-card v-for="(rate,idx) in ratedDogs" :key="idx"  style="margin:5vh 2vh">
        <a :href="rate.dog">
          <img :src="rate.dog" alt="" width="300px" style="margin:10px 0">                          
        </a>
        <div my-2 py-2>
          Rating
          <h4>            
            {{rate.rating}}
          </h4>
        </div>
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

</style>
