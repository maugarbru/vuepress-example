<template>
  <v-stepper v-model="e6" vertical>
    <v-stepper-step :complete="e6 > 1" step="1">
      Subir archivo de datos
      <small>Archivo .xls o .csv</small>
    </v-stepper-step>

    <v-stepper-content step="1">
      <v-container>
        <v-file-input
          v-model="file"
          chips
          show-size
          label="Archivo de datos"
          placeholder="Sube tu archivo"
          prepend-icon="mdi-file-excel"
        ></v-file-input>
        <v-btn :disabled="!file" outlined color="primary" @click="e6 = 2">
          Calcular
        </v-btn>
      </v-container>
    </v-stepper-content>

    <v-stepper-step :complete="e6 > 2" step="2">
      Calcular pérdida
    </v-stepper-step>

    <v-stepper-content step="2">
      <v-card color="grey lighten-1" class="mb-12" height="200px"></v-card>
    </v-stepper-content>

    <v-stepper-step :complete="e6 > 3" step="3">
      Ver resultados
    </v-stepper-step>

    <v-stepper-content step="3">
      <v-card color="grey lighten-1" class="mb-12" height="200px"></v-card>
      <v-btn color="primary" @click="e6 = 4"> Continue </v-btn>
      <v-btn text> Cancel </v-btn>
    </v-stepper-content>

    <v-stepper-step step="4"> Generar reporte </v-stepper-step>
    <v-stepper-content step="4">
      <v-card color="grey lighten-1" class="mb-12" height="200px"></v-card>
      <v-btn color="primary" @click="e6 = 1"> Continue </v-btn>
      <v-btn text> Cancel </v-btn>
    </v-stepper-content>
  </v-stepper>
</template>

<script>
export default {
  data() {
    return {
      e6: 1,
      file: null,
    };
  },
};
</script>