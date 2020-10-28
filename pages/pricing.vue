<template>
  <v-layout column justify-center align-center>
    <v-container width="500">
      <v-row xs12>
        <v-col cols="12" md="12">
          <v-card max-width="700" flat class="mx-auto">
            <v-list-item three-line>
              <v-list-item-content>
                <div class="overline mb-4 primary--text">
                  <i>PLANES QUE OFRECEMOS</i>
                </div>
                <v-list-item-title class="headline mb-1 success--text"
                  >PRECIOS</v-list-item-title
                >
              </v-list-item-content>
            </v-list-item>

            <v-card-text
              align="justify"
              style="font-size: 1rem; font-weight: 400; line-height: 1.5"
            >
              Disponemos de los siguentes planes dependiendo de las necesidades
              que usted tenga en su negocio y en su empresa
            </v-card-text>

            <v-expansion-panels multiple popout focusable hover tile>
              <!-- VIH -->
              <v-expansion-panel>
                <v-expansion-panel-header class="primary--text"
                  >Plan Básico</v-expansion-panel-header
                >
                <v-expansion-panel-content>
                  <v-card flat>
                    <v-card-title class="primary--text">Incluye:</v-card-title>
                    <v-card-text
                      align="justify"
                      style="
                        font-size: 1rem;
                        font-weight: 400;
                        line-height: 1.5;
                      "
                    >
                      El plan básico incluye sólo las operaciones de cálculos de
                      riesgos financieros.
                    </v-card-text>
                    <v-card-title class="success--text"
                      >$5 per month</v-card-title
                    >
                  </v-card>
                </v-expansion-panel-content>
              </v-expansion-panel>

              <!-- Cardiovascular -->
              <v-expansion-panel>
                <v-expansion-panel-header class="primary--text"
                  >Plan Completo</v-expansion-panel-header
                >
                <v-expansion-panel-content>
                  <v-card flat>
                    <v-card-title class="primary--text">Incluye:</v-card-title>
                    <v-card-text
                      align="justify"
                      style="
                        font-size: 1rem;
                        font-weight: 400;
                        line-height: 1.5;
                      "
                    >
                      Este plan incluye todas las operaciones de cálculos de
                      riesgos financieros y también la entrega de los reportes
                    </v-card-text>
                    <v-card-title class="success--text"
                      >$10 per month</v-card-title
                    >
                  </v-card>
                </v-expansion-panel-content>
              </v-expansion-panel>
            </v-expansion-panels>

            <v-card-text
              align="justify"
              style="font-size: 1rem; font-weight: 400; line-height: 1.5"
            >
              Esta atención pretende integrar un conjunto de servicios de
              promoción, prevención y asistencia a usuarios, grupos de personas
              en su entorno biopsicosocial.
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-layout>
</template>

<script>
export default {
  data() {
    return {};
  },
};
</script>