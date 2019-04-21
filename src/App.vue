<template>
  <v-app>
    <Nav></Nav>
    <router-view></router-view>
  </v-app>
</template>

<script>
import Nav from './components/Nav'
export default {
  components:{
    Nav
  },
  name: 'App',  
  data () {
    return {
      //
    }
  }
}
</script>
