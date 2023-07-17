<script setup lang="ts">
definePageMeta({
  layout: 'auth'
})

const form = ref('signIn')

const user = useSupabaseUser()

watchEffect(() => {
  if (user.value) {
    navigateTo('/teams')
  }
})
</script>

<template>
  <div>
    <h1 class="text-center mb-4">
      Team Manager
    </h1>

    <ul class="nav nav-tabs nav-fill mb-3">
      <li class="nav-item">
        <a
          class="nav-link"
          :class="{active: 'signIn' === form}"
          href="#"
          @click.prevent="form = 'signIn'"
        >
          Sign in
        </a>
      </li>

      <li class="nav-item">
        <a
          class="nav-link"
          :class="{active: 'signUp' === form}"
          href="#"
          @click.prevent="form = 'signUp'"
        >
          Sign up
        </a>
      </li>
    </ul>

    <FormSignIn v-if="'signIn' === form" />

    <FormSignUp v-if="'signUp' === form" />
  </div>
</template>
