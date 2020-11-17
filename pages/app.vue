<template>
  <v-container>
    <v-dialog v-model="dialog" persistent max-width="500">
      <auth v-if="dialog" @login="login" />
    </v-dialog>
    <v-card outlined v-if="user" class="mx-auto">
      <v-app-bar color="transparent" dense flat>
        <h2 class="primary--text">Bienvenido</h2>
        <v-spacer></v-spacer>
        <v-btn @click="cerrarSesion()" small color="red" outlined
          >Cerrar sesión
          <v-icon right>mdi-account-remove-outline</v-icon></v-btn
        >
      </v-app-bar>
      <v-card-text>
        <v-simple-table>
          <template v-slot:default>
            <tbody>
              <tr>
                <td align="right">
                  <v-icon color="success" left>mdi-domain</v-icon
                  ><b class="success--text mr-4">Compañía</b>
                </td>
                <td>{{ user.companyName }}</td>
              </tr>
              <tr>
                <td align="right">
                  <v-icon color="success" left>mdi-account</v-icon
                  ><b class="success--text mr-4">Usuario</b>
                </td>
                <td>{{ user.userName }}</td>
              </tr>
              <tr>
                <td align="right">
                  <v-icon color="success" left>mdi-email</v-icon
                  ><b class="success--text mr-4">E-mail</b>
                </td>
                <td>{{ user.email }}</td>
              </tr>
            </tbody>
          </template>
        </v-simple-table>
      </v-card-text>
    </v-card>
    <br />
    <v-card>
      <v-tabs
        v-model="tab"
        background-color="grey lighten-3"
        color="primary"
        grow
      >
        <v-tab> Pérdida </v-tab>
        <v-tab> Recuperación </v-tab>
      </v-tabs>

      <v-tabs-items v-model="tab">
        <v-tab-item>
          <v-card flat>
            <loss />
          </v-card>
        </v-tab-item>
        <v-tab-item>
          <v-card flat>
            <recovery />
          </v-card>
        </v-tab-item>
      </v-tabs-items>
    </v-card>
  </v-container>
</template>

<script>
import Auth from "@/components/Auth.vue";
import Loss from "@/components/Loss.vue";
import Recovery from "@/components/Recovery.vue";

export default {
  components: {
    Auth,
    Loss,
    Recovery
  },
  layout: "app",
  data() {
    return {
      tab: 0,
      dialog: true,
      user: undefined,
    };
  },
  methods: {
    login(validate) {
      if (validate.login) {
        this.dialog = false;
        this.user = validate.user;
      }
    },

    cerrarSesion() {
      this.user = undefined;
      this.dialog = true;
    },
  },
};
</script>