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
        <LoginForm />
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
};
</script>

<style scoped>
.img-bg {
  background-image: url("./assets/wobiz-bg.png");
  background-position: right bottom;
}
</style>
