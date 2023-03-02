<template>
  <v-card class="mx-auto" width="400">
    <v-card-item>
      <v-card-title class="mb-4">Login</v-card-title>
      <v-form fast-fail @submit.prevent="login">
        <v-text-field type="text" autocomplete="username" :class="{ 'invalid': $v.email.$error }" v-model="form.email"
          label="Email" />
        <template v-if="$v.$error">
          <p class="invalid-message" v-if="$v.email.required.$invalid">Email is required</p>
          <p class="invalid-message" v-else-if="$v.email.email.$invalid">Email format is wrong</p>
        </template>
        <v-text-field type="password" autocomplete="current-password" :class="{ 'invalid': $v.password.$error }"
          v-model="form.password" label="Password" />
        <template v-if="$v.$error">
          <p class="invalid-message" v-if="$v.password.required.$invalid">Password is required</p>
          <p class="invalid-message" v-else-if="$v.password.minLength.$invalid">Password should contain at least 6
            characters</p>
        </template>
        <v-btn type="submit" block class="mt-2">Submit</v-btn>
      </v-form>
    </v-card-item>
  </v-card>
</template>

<script setup>
import { useVuelidate } from '@vuelidate/core'
import { required, minLength, email } from '@vuelidate/validators'
import { reactive } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

const form = reactive({
  email: '',
  password: ''
})

const rules = {
  email: { required, email },
  password: { required, minLength: minLength(6) }
}

const $v = useVuelidate(rules, form)

const login = () => {
  $v.value.$touch()
  if ($v.value.$invalid) return
  router.push('/cards')
}
</script>

<style>
.invalid-message {
  color: red;
  margin-top: -18px;
  margin-bottom: 18px;
}

.invalid .v-field-label {
  color: red;
}

.invalid .v-field--variant-filled .v-field__outline::before {
  border-color: red;
}

.invalid .v-field--variant-filled .v-field__outline::after {
  border-color: red;
}
</style>