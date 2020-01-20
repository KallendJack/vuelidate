<template>
  <div>
    <form @submit.prevent="submit">
      <input
        type="text"
        name="firstname"
        placeholder="First Name"
        v-model="formInputs.firstName"
        :class="{ error: $v.formInputs.firstName.$error }"
        @blur="$v.formInputs.firstName.$touch()"
      />
      <div v-if="$v.formInputs.firstName.$error">
        <p v-if="!$v.formInputs.firstName.required">First name is required.</p>
      </div>
      <br />
      <input
        type="text"
        name="lastname"
        placeholder="Last Name"
        v-model="formInputs.lastName"
        :class="{ error: $v.formInputs.lastName.$error }"
        @blur="$v.formInputs.lastName.$touch()"
      />
      <div v-if="$v.formInputs.lastName.$error">
        <p v-if="!$v.formInputs.lastName.required">Last name is required.</p>
      </div>
      <br />
      <input
        type="email"
        name="email"
        placeholder="Email"
        v-model="formInputs.email"
        :class="{ error: $v.formInputs.email.$error }"
        @blur="$v.formInputs.email.$touch()"
      />
      <div v-if="$v.formInputs.email.$error">
        <p v-if="!$v.formInputs.email.email">
          Please enter a valid email address.
        </p>
        <p v-if="!$v.formInputs.email.required">Email is required.</p>
      </div>
      <br />
      <input
        type="text"
        name="subject"
        placeholder="Subject"
        v-model="formInputs.subject"
        :class="{ error: $v.formInputs.subject.$error }"
        @blur="$v.formInputs.subject.$touch()"
      />
      <div v-if="$v.formInputs.subject.$error">
        <p v-if="!$v.formInputs.subject.required">Subject is required.</p>
      </div>
      <br />
      <input
        type="textarea"
        name="message"
        placeholder="Message"
        v-model="formInputs.message"
        :class="{ error: $v.formInputs.message.$error }"
        @blur="$v.formInputs.message.$touch()"
      />
      <div v-if="$v.formInputs.message.$error">
        <p v-if="!$v.formInputs.message.required">Message is required.</p>
      </div>
      <br />
      <input
        class="button"
        type="submit"
        value="Submit"
        :disabled="$v.formInputs.$invalid"
      />
      <p v-if="$v.formInputs.$anyError" class="errorMessage">
        Please fill out the required field(s).
      </p>
    </form>
  </div>
</template>

<script>
import { required, email } from "vuelidate/lib/validators";

export default {
  data() {
    return {
      formInputs: {
        firstName: null,
        lastName: null,
        email: null,
        subject: null,
        message: null
      }
    };
  },
  validations: {
    formInputs: {
      firstName: { required },
      lastName: { required },
      email: { required, email },
      subject: { required },
      message: { required }
    }
  },
  methods: {
    submit() {
      this.$v.$touch();
      if (!this.$v.$invalid) {
        console.log("Form Submission");
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
input[type="text"],
input[type="email"] {
  width: 100%;
  max-width: 800px;
  padding: 12px 20px;
  margin: 8px 0;
  box-sizing: border-box;
}

input[type="textarea"] {
  width: 100%;
  max-width: 800px;
  height: 100px;
  padding: 12px 20px;
  margin: 8px 0;
  box-sizing: border-box;
}

input[type="submit"] {
  background-color: #4caf50;
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;

  &:disabled {
    background-color: lightgray;
  }
}

.error {
  border: 2px solid red;
}
</style>
