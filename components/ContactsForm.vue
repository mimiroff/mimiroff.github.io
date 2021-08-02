<template>
  <v-form ref="form" v-model="isValid" class="contacts-form">
    <v-text-field v-model="email" label="Email" outlined :rules="emailRules"></v-text-field>
    <v-text-field v-model="name" label="Name" outlined></v-text-field>
    <v-text-field v-model="subject" label="Subject" outlined></v-text-field>
    <v-textarea v-model="description" label="Description" outlined></v-textarea>
    <div class="d-flex justify-center mt-2">
      <v-alert v-if="shouldShowAlert" outlined color="white" max-width="600px" width="100%" dense :type="alertType">{{ alertText }}</v-alert>
      <v-btn v-else max-width="600px" width="100%" x-large outlined @click="submit">Submit</v-btn>
    </div>
  </v-form>
</template>

<script>
const fiveThousandMilliseconds = 5000;

export default {
  data() {
    return {
      email: '',
      name: '',
      subject: '',
      description: '',
      isValid: false,
      shouldShowAlert: false,
      alertText: '',
      alertType: null,
      emailRules: [
        (value) => !!value || 'Required.',
        (value) => {
        const pattern = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
        return pattern.test(value) || 'Invalid e-mail.';
      },]
    }
  },
  methods: {
    async submit() {
      this.$refs.form.validate()
      if (!this.isValid) {
        return
      }
      try {
        const { email, name, subject, description } = this;
        const res = await this.$axios.post('https://personal-6b588-default-rtdb.firebaseio.com/contacts.json', { email, name, subject, description })
        if (res.status === 200) {
          this.showSuccessAlert()
        } else {
          this.showErrorAlert()
        }
      } catch (ex) {
        this.showErrorAlert()
      }
    },
    showSuccessAlert() {
      this.alertType = 'success'
      this.alertText = 'Thank you! Your message has been received!'
      this.showAlert()
    },
    showErrorAlert() {
      this.alertType = 'error'
      this.alertText = 'Something went wrong! Please try again later.'
      this.showAlert()
    },
    showAlert() {
      this.shouldShowAlert = true
      setTimeout(() => {
        this.shouldShowAlert = false
        this.alertText = null
        this.alertType = null
      }, fiveThousandMilliseconds)
    }
  }
}
</script>
