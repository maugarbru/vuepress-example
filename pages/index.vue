<template>
  <div>
    <v-container>
      <v-parallax dark :height="200" :src="require('~/assets/fondo1.jpg')">
        <v-row align="center" justify="center">
          <v-col class="text-center" cols="12">
            <h1 class="display-1 font-weight-thin mb-4">
              Empieza con nosotros
            </h1>
            <v-btn class="primary--text" color="secondary" to="/app"
              >Ir a la app <v-icon right>mdi-application-import</v-icon></v-btn
            >
          </v-col>
        </v-row>
      </v-parallax>
    </v-container>

    <v-layout justify-center align-center>
      <v-item-group>
        <v-container>
          <v-row xs12>
            <v-col v-for="(item, index) in items" :key="index" cols="12" md="4">
              <v-item>
                <v-hover v-slot:default="{ hover }">
                  <v-card
                    class="mx-auto"
                    outlined
                    :to="item.to"
                    :elevation="hover ? 4 : 0"
                  >
                    <v-list-item three-line>
                      <v-list-item-content>
                        <div class="overline mb-4 primary--text">
                          {{ item.subtitle }}
                        </div>
                        <v-list-item-title
                          class="headline mb-1 success--text"
                          >{{ item.title }}</v-list-item-title
                        >
                        <v-list-item-subtitle>{{
                          item.description
                        }}</v-list-item-subtitle>
                      </v-list-item-content>
                    </v-list-item>
                    <v-container>
                      <center>
                        <v-img
                          v-if="index == 0"
                          max-width="450"
                          height="200"
                          contain
                          lazy-src
                          :src="require('~/assets/example1.jpg')"
                        ></v-img>
                        <v-img
                          v-if="index == 1"
                          max-width="450"
                          height="200"
                          contain
                          lazy-src
                          :src="require('~/assets/example2.jpg')"
                        ></v-img>
                        <v-img
                          v-if="index == 2"
                          max-width="450"
                          height="200"
                          contain
                          lazy-src
                          :src="require('~/assets/example3.jpg')"
                        ></v-img>
                      </center>
                    </v-container>
                  </v-card>
                </v-hover>
              </v-item>
            </v-col>
          </v-row>
        </v-container>
      </v-item-group>
    </v-layout>
  </div>
</template>

<script>
export default {
  components: {},
  data() {
    return {
      items: [
        {
          title: "Nuestro Servicio",
          subtitle: "API-RISK",
          to: "/info",
          img: "example1.jpg",
          description: "Acerca de API-RISK",
        },
        {
          title: "Nuestros Precios",
          subtitle: "Pricing",
          to: "/pricing",
          img: "example2.jpg",
          description: "Conoce nuestros planes",
        },
        {
          title: "Contáctenos",
          subtitle: "Contacto",
          to: "/contact",
          img: "example3.jpg",
          description: "Información de contacto",
        },
      ],
    };
  },
};
</script>