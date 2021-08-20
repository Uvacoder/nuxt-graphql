<template>
  <v-form ref="form" v-model="valid" lazy-validation :class="classProps">
    <v-container>
      <v-row>
        <v-col cols="12" class="py-0 my-0">
          <v-text-field v-model="email" :rules="emailRules" label="E-mail" type="email" outlined rounded dense required />
        </v-col>
        <v-col cols="6" class="py-0 my-0">
          <v-tooltip left>
            <template #activator="{ on, attrs }">
              <v-btn icon v-bind="attrs" @click="reset"  v-on="on">
                <v-icon>mdi-cached</v-icon>
              </v-btn>
            </template>
            <span>Reset form</span>
          </v-tooltip>
        </v-col>
        <v-col cols="6" align="right" class="py-0 my-0">
          <v-btn depressed rounded color="primary" :disabled="!valid" @click="validate">
            <v-icon left>mdi-send</v-icon> Send
          </v-btn>
        </v-col>
        <slot name="forget-password-form"></slot>
      </v-row>
    </v-container>
  </v-form>
</template>

<script>
export default {
  name: "ForgetPassword",
  props: {
    classProps: {
      type: String,
      default: 'forget-password-form',
      required: false
    }
  },
  data: () => ({
    valid: true,
    email: '',
    emailRules: [
      v => !!v || 'E-mail is required',
      v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
    ]
  }),

  methods: {
    validate() {
      if (this.$refs.form.validate()){
        this.$emit('reset-password-event','reset-password')
      }
    },
    reset() {
      this.$refs.form.reset()
    },
    resetValidation() {
      this.$refs.form.resetValidation()
    }
  }
}
</script>
