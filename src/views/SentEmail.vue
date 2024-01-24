<template>
  <div class="main">
    <h1>Gracias por comunicarse!</h1>
  </div>
</template>

<script>
import { onBeforeRouteLeave, onBeforeRouteUpdate } from "vue-router";
import axios from "axios";

export default {
  data() {
    return {
      nombre: "",
      correo: "",
      correoValido: false,
    };
  },
  methods: {
    enviarFormulario() {
      router.push({ path: "/sent-email" });
    },
    validar() {
      if (this.validarCorreo(this.correo)) {
        return true;
      } else {
        return false;
      }
    },
    validarCorreo(correo) {
      const expresionRegular = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      return expresionRegular.test(correo);
    },
    async obtenerDatos(variable) {
      try {
        const respuesta = await axios.get(
          `https://dc.oracleinfinity.io/e0a4074ec4a4477e0d7d61aa359ca278/dcs.gif?dcsdat=1705482148695&dcssip=e956-2806-10a6-19-8006-8ca2-d318-6a8a-a8bf.ngrok-free.app&dcsuri=%2F&wt.tz=-6&wt.bh=3&wt.ul=es-ES&wt.cd=24&wt.sr=1536x864&wt.jo=No&wt.ti=test-infinity&wt.js=Yes&wt.bs=599x703&wt.dl=0&wt.ssl=1&wt.es=e956-2806-10a6-19-8006-8ca2-d318-6a8a-a8bf.ngrok-free.app%2F&wt.tv=1.0.4&wt.ce=1&wt.co_f=bb081c43-fc02-498e-a873-d56dce850578&ora.tag_id=test_farolito_contact_tag&ora.tag_config=production&ora.fid=abc029a194ee4041e89b2c381e627486&ora.fid_tm=398&wt.abandono=true&wt.client_contact=${variable}`
        );
        console.log(respuesta);
      } catch (error) {
        console.error(error);
      }
    },
  },
  created() {
    onBeforeRouteLeave((to, from, next) => {
      const validaInputMail = new Promise((resolve) => {
        this.correo == ""
          ? (this.correoValido = false)
          : (this.correoValido = this.validar());
        console.log(this.correoValido);

        resolve();
      });

      validaInputMail.then(() => {
        this.correoValido ? this.obtenerDatos(this.correo) : "";
      });

      next();
    });

    // onBeforeRouteUpdate((to, from, next) => {
    //   alert("onBeforeRouteUpdate");

    //   next();
    // });
  },
};
</script>

<style lang="scss">
form {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 50px;
}

label {
  font-size: 18px;
  margin-bottom: 10px;
}

input {
  padding: 10px;
  border-radius: 5px;
  border: solid 1px black;
  margin-bottom: 20px;
  width: 300px;
  font-size: 16px;
}

button {
  background-color: #4caf50;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  font-size: 18px;
  cursor: pointer;
}

button:hover {
  background-color: #3e8e41;
}
</style>
