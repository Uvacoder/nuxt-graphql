<template>
  <v-form ref="form" v-model="valid" lazy-validation :class="classProps">
    <v-container>
      <v-row>
        <v-col cols="12" class="py-0 my-0">
          <v-text-field v-model="name" :rules="[v => !!v || 'Name is required.']" label="name" type="text" outlined rounded dense required />
          <v-text-field v-model="email" :rules="emailRules" label="E-mail" type="email" outlined rounded dense required />
          <v-text-field v-model="password" :rules="passwordRules" label="Password" type="password" outlined rounded dense required />
          <v-text-field v-model="confirmPassword" :rules="passwordRules.concat(passwordConfirmationRule)" label="Confirm Password" type="password" outlined rounded dense required />
          <v-checkbox v-model="checkbox" :rules="[v => !!v || 'You must agree to continue!']" label="Do you agree?" class="my-0" required />
        </v-col>
        <v-col cols="3" class="py-0 my-0">
          <v-tooltip left>
            <template #activator="{ on, attrs }">
              <v-btn icon v-bind="attrs" @click="reset" v-on="on">
                <v-icon>mdi-cached</v-icon>
              </v-btn>
            </template>
            <span>Reset login form</span>
          </v-tooltip>
        </v-col>
        <v-col cols="9" align="right" class="py-0 my-0">
          <v-btn depressed rounded color="primary" app :disabled="!valid" @click="validate">
            <v-icon left>mdi-login</v-icon> Register
          </v-btn>
        </v-col>
        <slot name="register-links"></slot>
      </v-row>
    </v-container>
  </v-form>
</template>

<script>
export default {
  name: "Register",
  props: {
    classProps: {
      type: String,
      default: 'register-form',
      required: false
    }
  },
  data: () => ({
    valid: true,
    name: '',
    email: '',
    emailRules: [
      v => !!v || 'E-mail is required',
      v => /.+@.+\..+/.test(v) || 'E-mail must be valid'
    ],
    password: '',
    passwordRules: [
      v => !!v || 'Password is required',
      v => /(?=.*\d)/.test(v) || 'Password must contain a number.',
      v => /(?=.*[a-z])/.test(v) || 'Password must contain a lowercase alphabet.',
      v => /(?=.*[A-Z])/.test(v) || 'Password must contain a uppercase alphabet.',
      v => /(?=.*[!@#$%^&*+=])/.test(v) || 'Password must contain one of !@#$%^&*+= characters.',
      v => (v && v.length > 7) || 'Password must be eight character long.',
    ],
    confirmPassword:'',
    checkbox: false,
  }),
  computed: {
    passwordConfirmationRule() {
      return () => (this.password === this.confirmPassword) || 'Password must match'
    },
  },
  methods: {
    validate() {
      this.$refs.form.validate()
    },
    reset() {
      this.$refs.form.reset()
    },
    resetValidation() {
      this.$refs.form.resetValidation()
    }
  },
}
</script>

<style scoped>

</style>
