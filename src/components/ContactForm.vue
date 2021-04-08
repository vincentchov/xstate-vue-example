<template>
  <div
    class="container d-flex flex-column justify-content-center align-items-center"
  >
    <b-button
      v-if="!showForm && !showConfirmCancellation && !showSuccessMessage"
      @click="openForm()"
      variant="primary"
    >
      Send us a message
    </b-button>

    <b-form v-if="showForm" id="submitForm" @submit.prevent="submit">
      <b-form-group label="Full name" label-for="full-name">
        <b-input
          v-model="form.name"
          class="field"
          id="full-name"
          type="text"
          placeholder="Your full name"
        >
        </b-input>
      </b-form-group>

      <b-form-group label="E-mail" label-for="email">
        <b-input
          v-model="form.email"
          class="field"
          id="email"
          type="text"
          placeholder="Your e-mail address"
        />
      </b-form-group>

      <b-form-group label="Message" label-for="message">
        <b-form-textarea
          v-model="form.message"
          name="message"
          id="message"
          rows="5"
          placeholder="Type in your message"
          class="field"
        >
        </b-form-textarea>
      </b-form-group>

      <div class="d-flex justify-content-end">
        <b-button @click="cancelSubmission()" variant="secondary" class="mr-2">
          Cancel
        </b-button>
        <b-button
          form="submitForm"
          type="submit"
          variant="primary"
          :disabled="isSubmitting"
        >
          {{ isSubmitting ? "Submitting" : "Submit" }}
        </b-button>
      </div>
    </b-form>

    <div v-if="showConfirmCancellation">
      <div class="mb-3">
        Are you sure you want to cancel? Your form will be cleared.
      </div>

      <div class="d-flex justify-content-end">
        <b-button
          @click="cancelCancellation()"
          variant="secondary"
          class="mr-2"
        >
          No, go back.
        </b-button>

        <b-button @click="confirmCancellation()" variant="primary">
          Yes, cancel.
        </b-button>
      </div>
    </div>

    <div v-if="showSuccessMessage" class="text-green">
      <div class="mb-3">Hey! Thanks for your message!</div>
      <div class="d-flex justify-content-end">
        <b-button @click="sendAnotherMessage()" variant="primary">
          Send another message
        </b-button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data: () => {
    return {
      form: {
        name: null,
        email: null,
        message: null,
      },
      showForm: false,
      showConfirmCancellation: false,
      showSuccessMessage: false,
      isSubmitting: false,
    };
  },
  methods: {
    submit() {
      this.isSubmitting = true;
      return new Promise((resolve) => {
        setTimeout(() => resolve("success"), 1000);
      }).then(() => {
        this.isSubmitting = false;
        this.showForm = false;
        this.showSuccessMessage = true;
      });
    },
    openForm() {
      this.showForm = true;
    },
    cancelSubmission() {
      this.showConfirmCancellation = true;
      this.showForm = false;
    },
    cancelCancellation() {
      this.showForm = true;
      this.showConfirmCancellation = false;
    },
    confirmCancellation() {
      this.showForm = false;
      this.showConfirmCancellation = false;
      this.form.name = null;
      this.form.email = null;
      this.form.message = null;
    },
    sendAnotherMessage() {
      this.showForm = true;
      this.showSuccessMessage = false;
    },
  },
};
</script>

<style>
</style>