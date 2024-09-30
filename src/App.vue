<script>
import InputField from './components/InputField.vue';
import successIcon from "./assets/success.svg"
export default {
  components: { InputField },
  data() {
    return {
      userInfo: {
        firstName: "",
        lastName: "",
        email: "",
        queryType: "",
        message: "",
        isContactedWithTeam: false,
      },
      errors: {}, // Store field-specific errors as an object
      successMessageVisible: false, // Controls visibility of success message
    };
  },
  methods: {
    handleSubmit() {
      this.errors = {}; // Clear errors before validation

      // Validation rules
      if (!this.userInfo.firstName) {
        this.errors.firstName = "First name is required";
      }
      if (!this.userInfo.lastName) {
        this.errors.lastName = "Last name is required";
      }
      if (!this.userInfo.email) {
        this.errors.email = "Email is required";
      } else if (!this.isValidEmail(this.userInfo.email)) {
        this.errors.email = "Invalid email format";
      }
      if (!this.userInfo.queryType) {
        this.errors.queryType = "Please select a query type";
      }
      if (!this.userInfo.message) {
        this.errors.message = "Message is required";
      }

      // If no errors, proceed with form submission
      if (Object.keys(this.errors).length === 0) {
        console.log("Form submitted:", this.userInfo);
        this.showSuccessMessage();
      }
    },
    isValidEmail(email) {
      const emailPattern = /^[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+$/;
      return emailPattern.test(email);
    },
    showSuccessMessage() {
      // Set the message visibility to true, then hide it after 3 seconds
      this.successMessageVisible = true;
      setTimeout(() => {
        this.successMessageVisible = false;
      }, 3000); // Hide after 3 seconds
    },
  }
};
</script>


<template>
  <div class="form-wrapper">
    <div :class="`success-message  ${successMessageVisible ? 'visible':''}`">
      <h2><img src="./assets/success.svg" alt="">Message Sent!</h2>
      <p>Thanks for completing the form. We’ll be in touch soon!</p>
    </div>
    <h1 class="form-title">Contact Us</h1>
    <form class="form" @submit.prevent="handleSubmit">
      <InputField
          v-model="userInfo.firstName"
          label="First name"
          type="text"
          required
          :error="errors.firstName"
      />
      <InputField
          v-model="userInfo.lastName"
          label="Last name"
          type="text"
          required
          :error="errors.lastName"
      />
      <InputField
          v-model="userInfo.email"
          label="Email"
          type="email"
          required
          :error="errors.email"
      />

      <InputField
          v-model="userInfo.queryType"
          label="Query Type"
          type="radio-group"
          required
          :options="[
        { label: 'General Enquiry', value: 'General Enquiry' },
        { label: 'Support Request', value: 'Support Request' }
      ]"
      />


<!--      <label class="label-radio">-->
<!--        Query Type-->
<!--      </label>-->
<!--      <InputField-->
<!--          v-model="userInfo.queryType"-->
<!--          label="General Enquiry"-->
<!--          type="radio"-->
<!--          value="General Enquiry"-->
<!--          :error="errors.queryType"-->
<!--      />-->
<!--      <InputField-->
<!--          v-model="userInfo.queryType"-->
<!--          label="Support Request"-->
<!--          type="radio"-->
<!--          value="Support Request"-->
<!--          :error="errors.queryType"-->
<!--      />-->

      <InputField
          v-model="userInfo.message"
          label="Message"
          type="textarea"
          required
          :error="errors.message"
      />

      <InputField
          v-model="userInfo.isContactedWithTeam"
          label="I consent to being contacted"
          required
          type="checkbox"
      />

      <button type="submit">Submit</button>
    </form>
  </div>
</template>


<style scoped>

</style>
<style scoped>
.form-wrapper {
  position: relative;
  padding: 20px;
}

/* Success message styling */

</style>
