<template>
  <v-app>
    <v-main>
      <v-app-bar class="primary" dense>
        <v-btn to="/" class="secondary--text" text><v-icon left>mdi-arrow-left</v-icon> volver</v-btn>
        <v-spacer></v-spacer>
        <v-toolbar-title class="white--text">API-RISK</v-toolbar-title>
        <v-spacer></v-spacer>
        <v-menu offset-y left bottom>
          <template v-slot:activator="{ on, attrs }">
            <v-btn class="secondary--text" text v-bind="attrs" v-on="on">
              Usuario <v-icon right>mdi-account</v-icon>
            </v-btn>
          </template>

          <v-list>
            <v-list-item>
              <v-btn text block tile color="red darken-3" to="/app">
                Cerrar sesión
              </v-btn>
            </v-list-item>
          </v-list>
        </v-menu>
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