<template>
  <v-card>
    <v-app-bar class="transparent" dense flat>
      <v-spacer></v-spacer>
      <v-btn to="/" class="red--text" text>
        Salir<v-icon right>mdi-exit-to-app</v-icon></v-btn
      >
    </v-app-bar>
    <v-card-title class="text-center justify-center py-6">
      <h1 class="font-weight-bold display-3 secondary--text">API-RISK</h1>
    </v-card-title>

    <v-tabs v-model="tab" background-color="grey lighten-3" color="primary" grow>
      <v-tab> Ingresar </v-tab>
      <v-tab> Registrarse </v-tab>
    </v-tabs>

    <v-tabs-items v-model="tab">
      <v-tab-item>
        <v-card flat>
          <v-card-text
            ><v-form ref="formLogIn" v-model="validLogIn" lazy-validation>
              <v-text-field
                v-model="username"
                label="Usuario"
                :rules="logInRules"
                required
              ></v-text-field>

              <v-text-field
                type="password"
                v-model="password"
                :rules="logInRules"
                label="Contraseña"
                required
              ></v-text-field>

              <v-btn
                block
                :loading="loading"
                :disabled="!validLogIn"
                color="green"
                class="mr-4 mt-4 white--text"
                @click="validateLogIn"
              >
                Ingresar
              </v-btn>

              <div class="mx-auto mt-3" align="center">
                <i>No te has registrado? <a @click="tab++">Házlo aquí</a></i>
              </div>
            </v-form></v-card-text
          >
        </v-card>
      </v-tab-item>
      <v-tab-item>
        <v-card flat>
          <v-card-text
            ><v-form ref="formRegister" v-model="validRegister" lazy-validation>
              <v-text-field
                v-model="companyRegister"
                label="Nombre de la compañía *"
                :rules="registerRules"
                required
              ></v-text-field>

              <v-text-field
                v-model="usernameRegister"
                label="Nombre de usuario *"
                :rules="registerRules"
                required
              ></v-text-field>

              <v-text-field
                v-model="emailRegister"
                label="Correo electrónico *"
                :rules="emailRules"
                required
              ></v-text-field>

              <v-text-field
                type="password"
                v-model="passwordRegister"
                :rules="registerRules"
                label="Contraseña *"
                required
              ></v-text-field>

              <v-text-field
                type="password"
                v-model="passwordConfirm"
                :rules="registerRules"
                label="Confirmar contraseña *"
                required
              ></v-text-field>

              <v-btn
                block
                :loading="loading"
                :disabled="!validRegister"
                color="green"
                class="mr-4 mt-4 white--text"
                @click="validateRegister"
              >
                Registrarse
              </v-btn>

              <div class="mx-auto mt-3" align="center">
                <i>Ya tienes una cuenta? <a @click="tab--">Ingrese aquí</a></i>
              </div>
            </v-form></v-card-text
          >
        </v-card>
      </v-tab-item>
    </v-tabs-items>
    <v-overlay absolute :opacity="1" color="green" :value="overlaySuccessLogin">
      <v-card color="transparent" flat>
        <v-card-text class="green white--text mx-auto my-auto">
          <div><h1>Ingreso exitoso.</h1></div>
          <div v-if="user" class="mt-4">
            <h2>Bienvenido, {{ user.companyName }}!</h2>
          </div>
        </v-card-text>
      </v-card>
    </v-overlay>
    <v-overlay
      absolute
      :opacity="1"
      color="primary"
      :value="overlaySuccessRegister"
    >
      <v-card color="transparent" flat>
        <v-card-text class="primary white--text mx-auto my-auto">
          <div><h1>Registro exitoso.</h1></div>
          <div class="mt-4">
            <h2>Ingrese ahora con sus credenciales.</h2>
          </div>
        </v-card-text>
      </v-card>
    </v-overlay>
    <v-overlay absolute :opacity="1" color="red darken-3" :value="overlayError">
      <v-card color="transparent" flat>
        <v-card-text class="red darken-3 white--text mx-auto my-auto">
          <div>
            <h3>{{ error }}</h3>
          </div>
        </v-card-text>
      </v-card>
    </v-overlay>
  </v-card>
</template>

<script>
export default {
  data() {
    return {
      loading: false,
      validLogIn: true,
      validRegister: true,
      overlaySuccessLogin: false,
      overlaySuccessRegister: false,
      overlayError: false,
      logInRules: [(v) => !!v || "Este campo es requerido"],
      registerRules: [
        (v) => !!v || "Este campo es requerido",
        (v) => v.length <= 6 || "Debe tener mínimo 6 caracteres",
      ],
      emailRules: [
        (v) => !!v || "E-mail es requerido",
        (v) => /.+@.+/.test(v) || "E-mail debe ser válido",
      ],
      tab: 0,
      error: "",
      username: "",
      password: "",
      companyRegister: "",
      usernameRegister: "",
      passwordRegister: "",
      passwordConfirm: "",
      emailRegister: "",
      user: undefined,
    };
  },
  methods: {
    mostrarError(texto) {
      let self = this;
      this.overlayError = true;
      this.error = texto;
      setTimeout(() => {
        self.overlayError = false;
        self.passwordConfirm = "";
      }, 1500);
    },
    limpiarCampos() {
      this.username = "";
      this.password = "";
      this.companyRegister = "";
      this.usernameRegister = "";
      this.passwordRegister = "";
      this.passwordConfirm = "";
      this.emailRegister = "";
    },
    validateLogIn() {
      if (this.$refs.formLogIn.validate()) {
        let self = this;
        this.overlaySuccessLogin = true;
        this.user = {
          userName: "test123",
          companyName: "Verdulistas",
          email: "test123@verdulistas.co",
        };
        setTimeout(() => {
          self.$emit("login", {
            login: true,
            user: self.user,
          });
        }, 2000);
      }
    },
    validateRegister() {
      if (this.$refs.formRegister.validate()) {
        if (this.passwordRegister == this.passwordConfirm) {
          const self = this;
          const usuario = this.usernameRegister;
          this.overlaySuccessRegister = true;
          this.limpiarCampos();
          this.username = usuario;
          this.tab = 0;
          setTimeout(() => {
            self.overlaySuccessRegister = false;
          }, 1500);
        } else {
          this.mostrarError("Las contraseñas no coinciden.");
        }
      }
    },
  },
};
</script>