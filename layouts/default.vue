<script setup lang="ts">
const authClient = useSupabaseAuthClient()

const signOutLoading = ref(false)

async function signOut () {
  signOutLoading.value = true
  await authClient.auth.signOut()
  navigateTo('/')
}
</script>

<template>
  <div class="py-5">
    <div class="container">
      <slot />

      <div class="mt-5 text-center">
        <AppButton
          tag="button"
          label="Sign out"
          icon="fas fa-sign-out"
          icon-position="right"
          size="sm"
          variant="secondary"
          :loading="signOutLoading"
          @click="signOut"
        />
      </div>
    </div>
  </div>
</template>
