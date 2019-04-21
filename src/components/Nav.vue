<template>
   <v-toolbar>    
    <v-toolbar-title>Dog Rating</v-toolbar-title>
    <v-spacer></v-spacer>
    <v-toolbar-items class="hidden-sm-and-down">
      <v-btn flat :to="{name:'rateDogs'}">Rate Dogs</v-btn>
      <v-btn flat :to="{name:'dashboard'}">Dashboard</v-btn>      
    </v-toolbar-items>
    <div class="text-xs-center">
    <v-menu offset-y >
      <template v-slot:activator="{ on }" >        
        <v-icon v-on='on' class="hidden-md-and-up">mdi_menu</v-icon>        
      </template>
      <v-list>
        <v-flex align-center justify-center pa-1>
          <v-list-tile flat :to="{name:'rateDogs'}"> Rate Dogs</v-list-tile>
          <v-list-tile flat :to="{name:'dashboard'}">Dashboard</v-list-tile>    
        </v-flex>      
      </v-list>
    </v-menu>
  </div>
  </v-toolbar>
</template>

<script>
export default {

}
</script>

<style>

</style>
