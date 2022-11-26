<template>
  <div id="app">
    <v-app id="inspire">
      <v-toolbar>
        <v-app-bar-nav-icon></v-app-bar-nav-icon>
        <v-toolbar-title>Title</v-toolbar-title>
        <v-spacer></v-spacer>
        <v-toolbar-items class="hidden-sm-and-down">
          <v-btn text>Link One</v-btn>
          <v-btn text>Link Two</v-btn>
          <v-btn text>Link Three</v-btn>
        </v-toolbar-items>
      </v-toolbar>
      <v-main>
      <v-container>
        <Nuxt />
      </v-container>
      </v-main>
    </v-app>
  </div>

</template>

<style>
.v-toolbar {
  max-height: 60px;
}
.v-card {
        padding: 30px;
}
</style>

