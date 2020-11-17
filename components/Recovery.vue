<template>
  <v-stepper v-model="step" vertical>
    <v-stepper-step color="secondary" :complete="step > 1" step="1">
      Escoger pérdida
      <small>Pérdida a la cuál se le va a calcular la recuperación</small>
    </v-stepper-step>

    <v-stepper-content step="1">
      <v-card flat>
        <v-card-text>
          <v-select
            :items="items"
            :disabled="items.length == 0"
            label="Pérdidas"
            prepend-icon="mdi-file"
          ></v-select>
          <div v-if="items.length == 0" class="red--text">
            No tiene pérdidas calculadas para generar la recuperación.
          </div>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            v-if="items.length == 0"
            outlined
            small
            color="primary"
            @click="volverPerdida()"
          >
            <v-icon left>mdi-arrow-left</v-icon>Pérdida
          </v-btn>
          <v-btn
            :disabled="!loss || items.length == 0"
            outlined
            small
            color="primary"
            @click="calcularRecuperacion()"
          >
            Calcular <v-icon right>mdi-calculator-variant</v-icon>
          </v-btn>
          <v-spacer></v-spacer>
        </v-card-actions>
      </v-card>
    </v-stepper-content>

    <v-stepper-step color="secondary" :complete="step > 2" step="2">
      Calcular recuperación
    </v-stepper-step>

    <v-stepper-content step="2">
      <v-container>
        <h4>Obteniendo datos...</h4>
        <v-progress-linear
          align="center"
          :size="50"
          color="primary"
          rounded
          indeterminate
        ></v-progress-linear>
      </v-container>
    </v-stepper-content>

    <v-stepper-step color="secondary" :complete="step > 3" step="3">
      Ver resultados
    </v-stepper-step>

    <v-stepper-content step="3">
      <v-card flat class="mx-auto">
        <v-card-title>
          <h3 class="primary--text">Resultados</h3>
          <v-spacer></v-spacer>
          <h3 class="secondary--text">Recuperación: {{ recovery }}</h3>
        </v-card-title>
        <v-card-text v-if="loss">
          Resultados obtenidos a partir de los datos suministrados en el archivo
          <b
            ><i>{{ loss.name }}</i></b
          >
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn small outlined color="primary" @click="generarReporte()">
            Ver reporte
          </v-btn>
          <v-spacer></v-spacer>
        </v-card-actions>
      </v-card>
    </v-stepper-content>

    <v-stepper-step color="secondary" step="4">
      Generar reporte
    </v-stepper-step>
    <v-stepper-content step="4">
      <v-container v-if="loading">
        <h4>Obteniendo reporte...</h4>
        <v-progress-linear
          align="center"
          :size="50"
          color="primary"
          rounded
          indeterminate
        ></v-progress-linear>
      </v-container>
      <v-card v-else flat class="mx-auto">
        <v-card-title>
          <h3 class="primary--text">Reporte</h3>
          <v-spacer></v-spacer>
          <v-btn small tile color="secondary"
            >Descargar <v-icon right>mdi-download</v-icon></v-btn
          >
        </v-card-title>
        <v-card-text v-if="loss">
          Archivo de reporte generado de los datos de
          <b
            ><i>{{ loss.name }}</i></b
          >
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn small outlined color="primary" @click="step--"
            >Volver <v-icon right>mdi-arrow-up</v-icon></v-btn
          >
          <v-btn small outlined color="secondary" @click="iniciarProceso()"
            >Reiniciar<v-icon right>mdi-restart</v-icon></v-btn
          >
          <v-spacer></v-spacer>
        </v-card-actions>
      </v-card>
    </v-stepper-content>
  </v-stepper>
</template>

<script>
export default {
  data() {
    return {
      step: 1,
      items: [],
      loss: undefined,
      recovery: "",
      loading: false,
      report: undefined,
      error: false,
    };
  },
  methods: {
    calcularRecuperacion() {
      let self = this;
      this.error = false;
      this.step = 2;
      this.recovery = 212312;
      setTimeout(() => {
        self.step = 3;
      }, 2000);
    },

    generarReporte() {
      this.step = 4;
      if (!this.report) {
        let self = this;
        this.loading = true;
        setTimeout(() => {
          self.loading = false;
        }, 2000);
        this.report = 1;
      }
    },

    volverPerdida() {
      this.$emit("perdida");
    },

    iniciarProceso() {
      this.recovery = undefined;
      this.loss = undefined;
      this.report = undefined;
      this.step = 1;
    },
  },
};
</script>