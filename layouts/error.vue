<template>
  <v-layout column justify-center align-center>
    <v-container width="500">
      <v-row xs12>
        <v-col cols="12" md="12">
          <v-card max-width="700" flat class="mx-auto">
            <v-list-item three-line>
              <v-list-item-content>
                <div class="overline mb-4 orange--text">
                  <i>¡ALGO HA SALIDO MAL!</i>
                </div>
                <v-list-item-title class="mb-1 error--text">
                  <h1 v-if="error.statusCode === 404">{{ pageNotFound }}</h1>
                  <h1 v-else>{{ otherError }}</h1>
                </v-list-item-title>
              </v-list-item-content>
            </v-list-item>

            <v-list>
              <v-list-item-group>
                <v-list-item to="/">
                  <v-list-item-icon>
                    <v-icon color="primary">home</v-icon>
                  </v-list-item-icon>
                  <v-list-item-content>
                    <v-list-item-title class="primary--text">Regresar a Incio</v-list-item-title>
                    <v-list-item-subtitle>Click aquí para regresar</v-list-item-subtitle>
                  </v-list-item-content>
                </v-list-item>
              </v-list-item-group>
            </v-list>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-layout>
</template>

<script>
export default {
  layout: "empty",
  props: {
    error: {
      type: Object,
      default: null,
    },
  },
  data() {
    return {
      pageNotFound: "404 Página no encontrada",
      otherError: "Ha ocurrido un error",
    };
  },
  head() {
    const title =
      this.error.statusCode === 404 ? this.pageNotFound : this.otherError;
    return {
      title,
    };
  },
};
</script>

<style scoped>
h1 {
  font-size: 20px;
}
</style>
