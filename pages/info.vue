<template>
  <v-layout column justify-center align-center>
    <v-item-group>
      <v-container width="500">
        <v-row xs12>
          <v-col cols="12" md="12">
            <v-item>
              <v-card class="mx-auto" max-width="700" flat>
                <v-list-item two-line>
                  <v-list-item-content>
                    <div class="overline mb-4 primary--text">
                      <i>¿QUÉ ES?</i>
                    </div>
                    <v-list-item-title class="headline mb-1 success--text"
                      >API-RISK</v-list-item-title
                    >
                  </v-list-item-content>
                </v-list-item>
                <v-card-text
                  align="justify"
                  style="font-size: 1rem; font-weight: 400; line-height: 1.5"
                >
                  API-RISK es una API que proporciona servicios de cálculo y
                  entrega de operaciones de riesgos financieros que pueden tener
                  las empresas, adaptable a los datos del negocio, manteniendo
                  siempre la propiedad sobre estos datos para así conseguir
                  información real que influya en el curso de la compañía.
                </v-card-text>
              </v-card>
            </v-item>
            <hr />
            <br />

            <v-item>
              <v-card class="mx-auto" max-width="700" flat>
                <v-list-item three-line>
                  <v-list-item-content>
                    <div class="overline mb-4 primary--text">
                      <i>CARACTERÍSTICAS</i>
                    </div>
                    <v-list-item-title class="headline mb-1 success--text"
                      >VENTAJAS</v-list-item-title
                    >
                  </v-list-item-content>
                </v-list-item>
                <v-card-text
                  align="justify"
                  style="font-size: 1rem; font-weight: 400; line-height: 1.5"
                >
                  Nuestro servicio se caracteriza por ser:
                  <v-list disabled>
                    <v-list-item-group>
                      <v-list-item>
                        <v-list-item-icon>
                          <v-icon color="primary" left>grade</v-icon>
                        </v-list-item-icon>
                        <v-list-item-content>
                          <v-list-item-title
                            >Personalizable a las necesidades de la
                            empresa</v-list-item-title
                          >
                        </v-list-item-content>
                      </v-list-item>
                      <v-list-item>
                        <v-list-item-icon>
                          <v-icon color="success" left>assessment</v-icon>
                        </v-list-item-icon>
                        <v-list-item-content>
                          <v-list-item-title
                            >Generación de reportes</v-list-item-title
                          >
                        </v-list-item-content>
                      </v-list-item>
                      <v-list-item>
                        <v-list-item-icon>
                          <v-icon color="primary" left>alarm_on</v-icon>
                        </v-list-item-icon>
                        <v-list-item-content>
                          <v-list-item-title
                            >Nos basamos en la información que ya ha
                            recopilado</v-list-item-title
                          >
                        </v-list-item-content>
                      </v-list-item>
                      <v-list-item>
                        <v-list-item-icon>
                          <v-icon color="success" left>accessibility</v-icon>
                        </v-list-item-icon>
                        <v-list-item-content>
                          <v-list-item-title>Fácil de usar</v-list-item-title>
                        </v-list-item-content>
                      </v-list-item>
                    </v-list-item-group>
                  </v-list>
                </v-card-text>
              </v-card>
            </v-item>
            <hr />
            <br />
          </v-col>
        </v-row>
      </v-container>
    </v-item-group>
  </v-layout>
</template>

<script>
export default {
  data() {
    return {
      loading: false,
    };
  },
  methods: {},
};
</script>