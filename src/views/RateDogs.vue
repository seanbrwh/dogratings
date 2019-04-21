<template>
  <div my-5>
    <v-flex row align-center justify-center class="text-xs-center" mt-3>
      <h1>Rate Dog</h1>
    </v-flex>          
    <v-layout column justify-center align-center my-1>      
      <v-select class="hidden-md-and-up"
        v-model="selectedBreed"
        :items="breeds"
        label="Select A Breed"
        style="width:90vw"
      ></v-select>      
      <v-select class="hidden-sm-and-down"
        v-model="selectedBreed"
        :items="breeds"
        label="Select A Breed"
        style="width:20vw"
      ></v-select>      
    </v-layout>    
    <v-layout column justify-center align-center mb-5>
      <img  :src="dog" alt="Random Dog Photo"  width="200px">      
      <v-btn color="primary" @click="getRandomPhoto">Get Random Photo</v-btn>
      <v-btn color="secondary" @click="getRandomBreedPhoto">Get Breed Photo</v-btn>
    </v-layout>
    <v-layout row align-center justify-center class="text-xs-center">
      <h3>Rate The Dog</h3>
    </v-layout>
    <v-layout row justify-center align-center py-3 wrap>
      <div v-for="(rate,idx) in rating" :key='idx'>        
        <v-btn @click="rateDog(rate)">{{rate}}</v-btn>        
      </div>
    </v-layout>
  </div>
</template>

<script>
import _ from 'lodash'
import axios from 'axios'
var ratings = []
export default {
  data(){
    return {
      breeds:[],
      dog:'',
      selectedBreed:'',       
      rating:[10,11,12,13,14,15,16]
    }
  },
  methods:{
    getRandomPhoto(){
      axios.get('https://dog.ceo/api/breeds/image/random').then(res=>{
        this.dog = res.data.message
      })
    },
    getRandomBreedPhoto(){
      axios.get(`https://dog.ceo/api/breed/${this.selectedBreed}/images/random`).then(res=>{
        this.dog = res.data.message
      })
    },
    rateDog(rating){
      var dogRating = {rating:rating, dog:this.dog, id:  Math.random().toString(36).substring(7)}
      ratings.push(dogRating)
      localStorage.setItem('dogRating',JSON.stringify(ratings))
      if(this.selectedBreed == ''){
        this.getRandomPhoto()
      }else{
        this.getRandomBreedPhoto()
      }
    }
  },
  computed:{
    
  },
  mounted(){
    axios.get('https://dog.ceo/api/breeds/list/all').then(res=>{
      console.log(res.data.message)
      for(var breed in res.data.message){
        if(typeof breed == 'string'){
          this.breeds.push(breed)
        }
      }
      this.breeds.push(res.data.message)
    })
    this.getRandomPhoto()
  },
  watch:{
    selectedBreed:function(oldVal, newVal){
      if(oldVal != newVal){
        this.getRandomBreedPhoto()
      }
    }
  }
}
</script>

<style scoped>
  
</style>
