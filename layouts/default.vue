<template>
  <v-app>
    <v-main>
      <v-app-bar height="100">
        <v-spacer></v-spacer>
        <v-toolbar-title>API-RISK</v-toolbar-title>

        <v-spacer></v-spacer>

        <v-btn
          class="d-none d-sm-flex"
          height="100"
          text
          color="primary"
          tile
          v-for="(item, index) in items"
          :key="index"
          :to="item.to"
          >{{ item.title }}</v-btn
        >

        <v-spacer></v-spacer>
        <v-spacer></v-spacer>
        <v-menu left bottom class="d-flex d-sm-none">
          <template v-slot:activator="{ on, attrs }">
            <v-btn icon v-bind="attrs" v-on="on" class="d-flex d-sm-none">
              <v-icon>menu</v-icon>
            </v-btn>
          </template>

          <v-list>
            <v-list-item
              v-for="(item, index) in items"
              :key="index"
              @click="() => {}"
            >
              <v-btn block text tile color="primary" :to="item.to">{{
                item.title
              }}</v-btn>
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
    return {
      items: [
        {
          title: "Inicio",
          to: "/",
        },
        {
          title: "Información",
          to: "/info",
        },
        {
          title: "Pricing",
          to: "/pricing",
        },
        {
          title: "Contáctenos",
          to: "/contact",
        },
      ],
    };
  },
};
</script>
