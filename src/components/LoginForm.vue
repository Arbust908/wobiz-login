<template>
  <form novalidate @submit.prevent="handleForm">
    <p v-if="sentError" class="text-danger fs-5 ps-2">
      {{ sentError }}
    </p>
    <InputGroup
      type="email"
      name="Usuario"
      placeholder="usuario@mail.com"
      required
      @change="changeName"
      :invalid="sentError !== null"
    />
    <InputGroup
      type="password"
      name="Contraseña"
      placeholder="contraseña123"
      required
      minlength="6"
      @change="changePassword"
      :invalid="sentError !== null"
    />
    <Btn
      v-if="sending"
      type="button"
      color="info"
      text="Enviando"
      class="w-100"
      disabled
    />
    <Btn v-else type="submit" color="primary" text="Ingresar" class="w-100" />
  </form>
</template>

<script>
import axios from "axios";
import InputGroup from "./InputGroup.vue";
import Btn from "./Btn.vue";

export default {
  name: "LoginForm",
  components: {
    InputGroup,
    Btn,
  },
  data() {
    return {
      name: "",
      password: "",
      sending: null,
      sentError: null,
    };
  },
  methods: {
    changeName(value) {
      this.name = value;
    },
    changePassword(value) {
      this.password = value;
    },
    handleForm(event) {
      this.sending = true;
      const form = event.target;
      if (form.checkValidity()) {
        console.log("submitting");
        const url = "https://admin.localwobiz.com/login";
        const user = {
          username: this.name,
          password: this.password,
        };
        this.sending = true;
        axios
          .post(url, user)
          .then((response) => {
            const status = response.status;
            const res = response.data;
            if (status === 200) {
              this.$emit("login", res);
            } else if (status === 401) {
              this.loginError(res);
            }
          })
          .catch((error) => {
            console.log(error);
          })
          .finally(() => {
            this.sending = false;
          });
      }
    },
    loginError(error) {
      // Recomendaria pone run error generico para no dar mas informacion de la necesaria
      this.sentError = error.message;
    },
  },
};
</script>
