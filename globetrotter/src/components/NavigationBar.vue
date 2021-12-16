<template>
  <v-app-bar app color="primary" dark>
    <div class="d-flex align-center">
      <router-link to="/" class="menu">
        <v-icon large color="blue darken-2"> mdi-message-text </v-icon>
      </router-link>
    </div>
    <v-spacer></v-spacer>
    <div>
      <v-btn color="primary" outlined :to="{ path: '/' }">
        <span class="menu">Home</span>
      </v-btn>
      <router-link to="/about">
        <v-btn color="primary" outlined>
          <span class="menu">About</span>
        </v-btn>
      </router-link>
      <v-btn color="primary" outlined :to="{ path: '/dashboard' }">
        <span class="menu">Dashboard</span>
      </v-btn>
      <v-btn color="primary" outlined :to="{ path: '/login' }">
        <span class="menu">Login</span>
      </v-btn>
    </div>
  </v-app-bar>
</template>

<script>
export default {
  name: "NavigationBar",
};
</script>

<style scoped>
.menu {
  color: #fff;
  text-decoration: none;
}
</style>
