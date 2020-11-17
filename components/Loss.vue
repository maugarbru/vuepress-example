<template>
  <v-stepper v-model="step" vertical>
    <v-stepper-step color="secondary" :complete="step > 1" step="1">
      Subir archivo de datos
      <small>Archivo .xls o .csv</small>
    </v-stepper-step>

    <v-stepper-content step="1">
      <v-card flat>
        <v-card-text>
          <v-file-input
            v-model="file"
            chips
            show-size
            label="Archivo de datos"
            placeholder="Sube tu archivo"
            prepend-icon="mdi-file-excel"
          ></v-file-input>
          <div v-if="error && file" class="red--text">
            El archivo no tiene un formato compatible. Debe ser .xls o .csv.
          </div>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            :disabled="!file"
            outlined
            color="primary"
            @click="calcularPerdida()"
          >
            Calcular <v-icon right>mdi-calculator-variant</v-icon>
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-stepper-content>

    <v-stepper-step color="secondary" :complete="step > 2" step="2">
      Calcular pérdida
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
          <h3 class="secondary--text">Pérdida: {{ loss }}</h3>
        </v-card-title>
        <v-card-text v-if="file">
          Resultados obtenidos a partir de los datos suministrados en el archivo
          <b
            ><i>{{ file.name }}</i></b
          >
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn outlined color="primary" @click="generarReporte()">
            Ver reporte
          </v-btn>
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
        <v-card-text v-if="file">
          Archivo de reporte generado de los datos de
          <b
            ><i>{{ file.name }}</i></b
          >
        </v-card-text>
        <v-card-actions>
          <v-btn outlined color="primary" @click="step--">Resultados</v-btn>
          <v-spacer></v-spacer>
          <v-btn outlined @click="iniciarProceso()"
            >Inicio <v-icon right>mdi-arrow-up</v-icon></v-btn
          >
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
      file: undefined,
      loss: "",
      loading: false,
      report: undefined,
      error: false,
    };
  },
  methods: {
    calcularPerdida() {
      let self = this;
      if (
        this.file.name.split(".")[1] == "xls" ||
        this.file.name.split(".")[1] == "xlsx" ||
        this.file.name.split(".")[1] == "csv"
      ) {
        this.error = false;
        this.step = 2;
        this.loss = 212312;
        setTimeout(() => {
          self.step = 3;
        }, 2000);
      } else {
        this.error = true;
        setTimeout(() => {
          self.error = false;
        }, 2000);
      }
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

    iniciarProceso() {
      this.file = undefined;
      this.report = undefined;
      this.step = 1;
    },
  },
};
</script>