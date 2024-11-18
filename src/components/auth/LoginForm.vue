<template>
  <q-layout>
    <q-page-container>
      <q-page class="flex flex-center q-pa-md" style="height: 100vh">
        <q-card-section>
          <h5>Inicio de sesi&oacute;n</h5>
        </q-card-section>
        <q-card-section>
          <q-input
            v-model="emailVlue"
            label="Usuario"
            standout="bg-teal text-white"
            outlined
            dense
          >
          </q-input>
          <q-input
            label="password"
            v-model="pwdValue"
            standout="bg-teal text-white"
            outlined
            type="password"
            dense
          ></q-input>
        </q-card-section>
        <q-card-section>
          <q-btn label="Login" color="primary" @click="inicioSesion" />
        </q-card-section>
      </q-page>
    </q-page-container>
  </q-layout>
</template>
<style></style>

<script>
export default {
  name: "LoginForm",
  data() {
    return {
      emailVlue: "",
      pwdValue: "",
    };
  },
  methods: {
    inicioSesion() {
      console.log("Click en el boton de inicio de sesion");
      console.log("Valor de email: " + this.emailVlue);

      let endpointLogin = "/api/User/SignIn";
      let user = { email: this.emailVlue, password: this.pwdValue };
      this.$api
        .post(endpointLogin, user)
        .then((response) => {
          //Respuesta exitosa
          console.log("Respuesta exitosa: " + JSON.stringify(response));
          this.$q.notify({
            message: "Bienvenido a Store APP",
            color: "positive",
            position: "bottom",
            timeout: 5000,
          });
          this.$router.push("/");
        })
        .catch((error) => {
          //Ocurrio un error
          this.$q.notify({
            message: "Ocurrio un error",
            color: "negative",
            position: "bottom",
            timeout: 5000,
          });
          console.log("Error en: " + error);
        });
    },
  },
};
</script>
