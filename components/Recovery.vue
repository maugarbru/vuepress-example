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
            v-model="lossSelected"
            :items="lossesNames"
            :disabled="lossesNames.length == 0"
            label="Pérdidas"
            prepend-icon="mdi-file"
          ></v-select>
          <div v-if="lossesNames.length == 0" class="red--text">
            No tiene pérdidas calculadas para generar la recuperación.
          </div>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            v-if="lossesNames.length == 0"
            outlined
            small
            color="primary"
            @click="volverPerdida()"
          >
            <v-icon left>mdi-arrow-left</v-icon>Pérdida
          </v-btn>
          <v-btn
            :disabled="!lossSelected || lossesNames.length == 0"
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
      <v-card v-if="recovery" flat class="mx-auto">
        <v-card-title>
          <h3 class="primary--text">Resultados</h3>
          <v-spacer></v-spacer>
          <h3 class="secondary--text">
            Recuperación: {{ recovery.recovery }}%
          </h3>
        </v-card-title>
        <v-card-text>
          Resultados obtenidos a partir de los datos suministrados.
        </v-card-text>
        <v-card-text>
          Informe de operación:
          <div>
            Pérdida:
            <b>{{ lossSelected }}</b>
          </div>
          <div>
            ID Recuperación: <b>{{ recovery.id }}</b>
          </div>
          <div>
            ID Entidad: <b>{{ recovery.entity_id }}</b>
          </div>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn small outlined color="primary" @click="generarReporte()">
            Ver reporte
          </v-btn>
          <v-spacer></v-spacer>
        </v-card-actions>
      </v-card>
      <v-alert v-if="error" dense outlined type="error">
        {{ error_text }}
      </v-alert>
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
          <v-btn small tile color="secondary" @click="descargarReporte()"
            >Descargar <v-icon right>mdi-download</v-icon></v-btn
          >
        </v-card-title>
        <v-card-text>
          Haga click en el botón DESCARGAR para obtener el PDF del reporte
          generado.
        </v-card-text>
        <v-card-text v-if="recovery">
          Informe de operación:
          <div>
            Pérdida:
            <b>{{ lossSelected }}</b>
          </div>
          <div>
            ID Recuperación: <b>{{ recovery.id }}</b>
          </div>
          <div>
            ID Entidad: <b>{{ recovery.entity_id }}</b>
          </div>
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
      <v-alert v-if="error" dense outlined type="error">
        {{ error_text }}
      </v-alert>
    </v-stepper-content>
  </v-stepper>
</template>

<script>
import config from "~/assets/config.js";
import axios from "axios";

export default {
  props: {
    losses: Array,
    lossesNames: Array,
  },
  data() {
    return {
      step: 1,
      loss: undefined,
      recovery: "",
      loading: false,
      report: undefined,
      error: false,
      error_text: "",
      lossSelected: undefined,
    };
  },
  methods: {
    async calcularRecuperacion() {
      let self = this;
      this.error = false;
      this.step = 2;
      this.loss = this.losses.filter((l) => l.name == this.lossSelected)[0];
      try {
        let url = config.api_url + this.loss.id + "/recovery";
        let prom = await axios.post(url);
      } catch (error) {
        console.log(error);
      }
      try {
        let url2 = config.api_url + this.loss.id + "/recovery";
        let prom2 = await axios.get(url2);
        this.error = false;
        this.step = 2;
        this.recovery = prom2.data.data.recovery;
        setTimeout(() => {
          self.step = 3;
        }, 2000);
      } catch (error) {
        this.error = true;
        this.error_text = error;
        console.log(error);
      }
      setTimeout(() => {
        self.step = 3;
      }, 2000);
    },

    async generarReporte() {
      this.step = 4;
      if (!this.report) {
        try {
          let url = config.api_url + this.loss.id + "/recovery/report";
          let prom = await axios.get(url);
          this.report = prom.data;
          let self = this;
          this.loading = true;
          setTimeout(() => {
            self.loading = false;
          }, 2000);
        } catch (error) {
          this.error = true;
          this.error_text = error;
          console.log(error);
        }
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

    descargarReporte() {
      const newBlob = new Blob([this.report], { type: "application/pdf" });

      // MS Edge and IE don't allow using a blob object directly as link href, instead it is necessary to use msSaveOrOpenBlob
      if (window.navigator && window.navigator.msSaveOrOpenBlob) {
        window.navigator.msSaveOrOpenBlob(newBlob);
      } else {
        // For other browsers: create a link pointing to the ObjectURL containing the blob.
        const objUrl = window.URL.createObjectURL(newBlob);

        let link = document.createElement("a");
        link.href = objUrl;
        link.download = `ReporteRecuperacion-[${
          this.loss.id
        }]-[${new Date().toLocaleDateString()}].pdf`;
        link.click();

        // For Firefox it is necessary to delay revoking the ObjectURL.
        setTimeout(() => {
          window.URL.revokeObjectURL(objUrl);
        }, 250);
      }
    },
  },
};
</script>