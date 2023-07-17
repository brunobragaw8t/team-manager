<script setup lang="ts">
defineProps<{
  tag: string
  label: string
  loading?: boolean
}>()
</script>

<template>
  <component :is="tag" class="btn btn-primary" :disabled="loading">
    <div v-if="loading" class="spinner-border" role="status">
      <span class="visually-hidden">Loading...</span>
    </div>

    {{ label }}
  </component>
</template>

<style scoped>
.spinner-border {
  width: 1rem;
  height: 1rem;
  margin-right: 0.5rem;
}
</style>
