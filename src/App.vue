<template>
  <v-app id="inspire">
    <v-app-bar color="primary" dark>
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      <v-app-bar-title class="app-bar-title">Svijet novosti</v-app-bar-title>
    </v-app-bar>

    <v-navigation-drawer
      v-model="drawer"
      temporary
      app
      color="secondary"
      class="pa-4">
      <v-list>
        <v-list-item class="v-list-item--link theme--dark">
          <router-link to="/" class="v-list-item__content">
            <v-list-item-title>Početna</v-list-item-title>
          </router-link>
        </v-list-item>
        <v-list-item class="v-list-item--link theme--dark">
          <router-link to="/topStories" class="v-list-item__content">
            <v-list-item-title>Top priče</v-list-item-title>
          </router-link>
        </v-list-item>
        <v-list-item class="v-list-item--link theme--dark">
          <router-link to="/about" class="v-list-item__content">
            <v-list-item-title>O nama</v-list-item-title>
          </router-link>
        </v-list-item>
        <v-list-item class="v-list-item--link theme--dark">
          <router-link to="/contact" class="v-list-item__content">
            <v-list-item-title>Kontakt</v-list-item-title>
          </router-link>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-main class="main-content">
      <v-container>
        <router-view></router-view>
      </v-container>
    </v-main>
  </v-app>
</template>

<script setup>
  import { ref } from 'vue';
  const drawer = ref(false);
</script>

<style scoped>
.v-app-bar {
  box-shadow: 0 2px 4px rgba(87, 86, 86, 0.1);
}

.v-navigation-drawer {
  width: 250px;
}

.main-content {
  background-color: #EEEEEE; 
}
.v-list-item__content {
  text-decoration: none;
  font-weight: bold; 
}

.app-bar-title {
  font-size: 1.5rem; 
  font-weight: 600; 
  letter-spacing: 0.5px; 
  color: #ffffff; 
}

.v-list-item a{
  color: white;
}

</style>
