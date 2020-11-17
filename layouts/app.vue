<template>
  <v-app>
    <v-main>
      <v-app-bar class="primary" dense>
        <v-spacer></v-spacer>
        <v-toolbar-title class="white--text">API-RISK</v-toolbar-title>
        <v-spacer></v-spacer>
        <v-btn to="/" class="secondary--text" text>
          Salir<v-icon right>mdi-exit-to-app</v-icon></v-btn
        >
      </v-app-bar>
      <v-container class="mb-20">
        <nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data() {
    return {};
  },
};
</script>