<template>
  <form novalidate @submit.prevent="handleForm">
    <InputGroup
      type="email"
      name="Usuario"
      placeholder="usuario@mail.com"
      required
      @change="changeName"
    />
    <InputGroup
      type="password"
      name="Contraseña"
      placeholder="contraseña123"
      required
      minlength="6"
      @change="changePassword"
    />
    <Btn type="submit" color="primary" text="Ingresar" />
  </form>
</template>

<script>
import axios from "axios";
import InputGroup from "./InputGroup.vue";
import Btn from "./Btn.vue";

export default {
  components: {
    InputGroup,
    Btn,
  },
  data() {
    return {
      name: "",
      password: "",
      sending: null,
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
      const form = event.target;
      if (form.checkValidity()) {
        console.log("submitting");
        const user = {
          username: this.name,
          password: this.password,
        };
        this.sending = true;
        axios
          .post("https://admin.localwobiz.com/login", user)
          .then((result) => {
            console.log(result);
          })
          .catch((error) => {
            console.log(error);
          })
          .finally(() => {
            this.sending = false;
          });
      }
    },
  },
};
</script>
