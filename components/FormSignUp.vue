<script setup lang="ts">
const authClient = useSupabaseAuthClient()

const credentials = ref({
  name: '',
  email: '',
  password: ''
})

const isLoading = ref(false)

const alert = ref({
  type: '',
  message: ''
})

async function signUp () {
  isLoading.value = true

  const { data, error } = await authClient.auth.signUp({
    email: credentials.value.email,
    password: credentials.value.password,
    options: {
      data: {
        name: credentials.value.name
      }
    }
  })

  isLoading.value = false

  if (error) {
    alert.value = {
      type: 'danger',
      message: error.message
    }

    return error
  }

  alert.value = {
    type: 'success',
    message: 'Account created successfully. Please check your email to validate your account.'
  }

  credentials.value = {
    name: '',
    email: '',
    password: ''
  }

  return data
}
</script>

<template>
  <form @submit.prevent="signUp">
    <div class="mb-3">
      <FormInput
        v-model="credentials.name"
        type="text"
        placeholder="Your name"
        label="Name"
        icon="far fa-user"
        :required="true"
        :focus="true"
      />
    </div>

    <div class="mb-3">
      <FormInput
        v-model="credentials.email"
        type="email"
        placeholder="example@email.com"
        label="Email"
        icon="far fa-envelope"
        :required="true"
      />
    </div>

    <div class="mb-3">
      <FormInput
        v-model="credentials.password"
        type="password"
        placeholder="Your secret password"
        label="Password"
        icon="fas fa-key"
        :required="true"
      />
    </div>

    <div v-if="alert.type" :class="`alert alert-${alert.type}`">
      {{ alert.message }}
    </div>

    <div class="d-flex justify-content-end">
      <AppButton tag="button" type="submit" label="Sign up" :loading="isLoading" />
    </div>
  </form>
</template>
