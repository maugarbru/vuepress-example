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
            small
            color="primary"
            @click="calcularPerdida()"
          >
            Calcular <v-icon right>mdi-calculator-variant</v-icon>
          </v-btn>
          <v-spacer></v-spacer>
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
      <v-card v-if="loss" flat class="mx-auto">
        <v-card-title>
          <h3 class="primary--text">Resultados</h3>
          <v-spacer></v-spacer>
          <h3 class="secondary--text">Pérdida: ${{ loss.quantity }}</h3>
        </v-card-title>
        <v-card-text v-if="file">
          Resultados obtenidos a partir de los datos suministrados.
        </v-card-text>
        <v-card-text v-if="file">
          Informe de operación:
          <div>
            Archivo:
            <b>{{ file.name }}</b>
          </div>
          <div>
            ID Pérdida: <b>{{ loss.id }}</b>
          </div>
          <div>
            ID Entidad: <b>{{ loss.entity_id }}</b>
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
        <v-card-text v-if="file">
          Haga click en el botón DESCARGAR para obtener el PDF del reporte
          generado.
        </v-card-text>
        <v-card-text v-if="file && loss">
          Informe de operación:
          <div>
            Archivo:
            <b>{{ file.name }}</b>
          </div>
          <div>
            ID Pérdida: <b>{{ loss.id }}</b>
          </div>
          <div>
            ID Entidad: <b>{{ loss.entity_id }}</b>
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
  data() {
    return {
      step: 1,
      file: undefined,
      loss: undefined,
      loading: false,
      report: undefined,
      error: false,
      error_text: "",
      lossID: undefined,
    };
  },
  methods: {
    async calcularPerdida() {
      let self = this;
      if (
        this.file.name.split(".")[1] == "xls" ||
        this.file.name.split(".")[1] == "xlsx" ||
        this.file.name.split(".")[1] == "csv"
      ) {
        let date = Date.now();
        this.lossID = "lost" + date;
        try {
          let url1 = config.api_url + this.lossID + "/file";
          let form_data = new FormData();
          form_data.append("file", this.file);
          let prom1 = await axios.post(url1, form_data, {
            headers: {
              "Content-Type": "multipart/form-data",
            },
          });
          let url2 = config.api_url + this.lossID;
          let prom2 = await axios.post(url2);
          let url3 = config.api_url + this.lossID;
          let prom3 = await axios.get(url3);
          this.error = false;
          this.step = 2;
          this.loss = prom3.data.data.lost;
          setTimeout(() => {
            self.step = 3;
          }, 2000);
          this.$emit("agregarPerdida", {
            id: this.lossID,
            name: `Perdida [${
              this.file.name
            }] - [${new Date().toLocaleDateString()}]`,
          });
        } catch (error) {
          this.error = true;
          this.error_text = error;
          console.log(error);
        }
      } else {
        this.error = true;
        setTimeout(() => {
          self.error = false;
        }, 2000);
      }
    },

    async generarReporte() {
      this.step = 4;
      if (!this.report) {
        try {
          let url = config.api_url + this.lossID + "/report";
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

    iniciarProceso() {
      this.file = undefined;
      this.report = undefined;
      this.lossID = "";
      this.loss = undefined;
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
        link.download = `ReportePerdida-[${
          this.file.name
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