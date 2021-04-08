<template>
  <div id="app">
    <div class="d-flex flex-column justify-content-center align-items-center">
      <h1>Original version</h1>
      <ContactForm />

      <h1>Xstate version</h1>
    </div>
  </div>
</template>

<script>
import ContactForm from "./components/ContactForm.vue";

export default {
  name: "App",
  components: {
    ContactForm,
  },
};
</script>
