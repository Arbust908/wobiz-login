<template>
  <main id="app" class="min-vh-100 position-relative container-fluid">
    <div class="row">
      <section
        class="img-bg top-0 bottom-0 start-0 end-0 position-absolute"
      ></section>
      <section class="p-4 position-relative bg-light col min-vh-100 col-md-4">
        <h1 title="Wobiz Logo" class="p-3">
          <img
            class="img-fluid"
            src="./assets/wobiz-logo.png"
            loading="lazy"
            alt="Logo"
          />
        </h1>
        <LoginForm v-if="user === null" @login="login" />
        <h2 v-else>{{ user }} estas logeado!</h2>
      </section>
    </div>
  </main>
</template>

<script>
import LoginForm from "./components/LoginForm.vue";

export default {
  name: "App",
  components: {
    LoginForm,
  },
  data() {
    return {
      user: null,
    };
  },
  methods: {
    login(data) {
      this.$cookies.set("user_id", data.user_id, data.expires);
      this.$cookies.set("token", data.token, data.expires);
      this.user = data.user_id;
    },
  },
};
</script>

<style scoped>
.img-bg {
  background-image: url("./assets/wobiz-bg.png");
  background-position: right bottom;
}
</style>
