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
      <v-btn color="primary" @click="getRandomPhoto" style="width:45vw">Get Random Photo</v-btn>
      <v-btn color="secondary" @click="getRandomBreedPhoto" style="width:45vw" :disabled="selectedBreed.length == 0">Get Breed Photo</v-btn>
    </v-layout>
    <v-layout row justify-center align-center style="width:80vw; margin: 0 auto" >
      <v-textarea outline label='Notes' v-model="notes"></v-textarea>
    </v-layout>
    <v-layout column align-center justify-center class="text-xs-center">
      <h3>Rate The Dog</h3>
      <v-layout row align-center class="text-xs-center">
        <div style="margin:0 10px">10 <v-icon>thumb_down</v-icon></div>
        <div style="margin:0 10px">16 <v-icon>thumb_up</v-icon></div>        
      </v-layout>        
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
      rating:[10,11,12,13,14,15,16],
      notes:''
    }
  },
  methods:{
    getRandomPhoto(){
      axios.get('https://dog.ceo/api/breeds/image/random').then(res=>{
        this.dog = res.data.message
      })
    },
    getRandomBreedPhoto(){
      if(this.selectedBreed.split(' ').length > 1){
        axios.get(`https://dog.ceo/api/breed/${this.selectedBreed.split(' ')[1]}/${this.selectedBreed.split(' ')[0]}/images/random`).then(res=>{
          this.dog = res.data.message
        })
      }else{
          axios.get(`https://dog.ceo/api/breed/${this.selectedBreed}/images/random`).then(res=>{
            this.dog = res.data.message
          })
      }
    },
    rateDog(rating){
      var dogRating = {rating:rating, dog:this.dog, id:  Math.random().toString(36).substring(7), Note:this.notes}
      ratings.push(dogRating)
      localStorage.setItem('dogRating',JSON.stringify(ratings))
      if(this.selectedBreed == ''){
        this.getRandomPhoto()
      }else{
        this.getRandomBreedPhoto()
      }
      this.notes = ''
    }
  },
  computed:{
    
  },
  mounted(){
    axios.get('https://dog.ceo/api/breeds/list/all').then(res=>{
      var finRes = Object.entries(res.data.message).map(e=>{
        if(e[1].length){          
          e = e[1].map(f=>`${f} ${e[0]}`)          
        }else{
          e = e[0]
        }
        return e
      })      
      this.breeds = _.flatten(finRes)      
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
  img{
    display: block;
    max-width: 70vw;
    width: auto;
  }
</style>
