<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
    
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          transition="scale-transition"
          width="40"
        />
        <v-toolbar-title>Message App</v-toolbar-title>       
      </div>
      <v-spacer></v-spacer>
      
     
    </v-app-bar>
     <v-content>
     <router-view/>
    </v-content>
  </v-app>
</template>

<script>

export default {
  name: 'App',

  components: {
  },

  data: () => ({
    //
  }),
};
</script>
