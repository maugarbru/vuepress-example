<template>
  <v-layout column justify-center align-center>
    <v-container width="500">
      <v-row xs12>
        <v-col cols="12" md="12">
          <v-card max-width="700" flat class="mx-auto">
            <v-list-item three-line>
              <v-list-item-content>
                <div class="overline mb-4 primary--text">
                  <i>INFORMACIÓN</i>
                </div>
                <v-list-item-title class="headline mb-1 success--text">CONTACTO</v-list-item-title>
              </v-list-item-content>

            </v-list-item>
            <v-list disabled>
              <v-list-item-group>
                <v-list-item >
                  <v-list-item-icon>
                    <v-icon color="primary">business</v-icon>
                  </v-list-item-icon>
                  <v-list-item-content>
                    <v-list-item-title>Sede</v-list-item-title>
                    <v-list-item-subtitle>Medellín - Colombia</v-list-item-subtitle>
                  </v-list-item-content>
                </v-list-item>

                <v-list-item>
                  <v-list-item-icon>
                    <v-icon color="secondary">email</v-icon>
                  </v-list-item-icon>
                  <v-list-item-content>
                    <v-list-item-title>E-mail</v-list-item-title>
                    <v-list-item-subtitle>contact@apirisk.co</v-list-item-subtitle>
                  </v-list-item-content>
                </v-list-item>

                <v-list-item>
                  <v-list-item-icon>
                    <v-icon color="primary">contact_phone</v-icon>
                  </v-list-item-icon>
                  <v-list-item-content>
                    <v-list-item-title>WhatsApp</v-list-item-title>
                    <v-list-item-subtitle>(+57) 312 657 0779</v-list-item-subtitle>
                  </v-list-item-content>
                </v-list-item>

                <v-list-item>
                  <v-list-item-icon>
                    <v-icon color="secondary">phone</v-icon>
                  </v-list-item-icon>
                  <v-list-item-content>
                    <v-list-item-title>Teléfono</v-list-item-title>
                    <v-list-item-subtitle>(+57) (4) 596 6025</v-list-item-subtitle>
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
  data() {
    return {};
  },
};
</script>