<script setup lang="ts">
defineProps<{
  tag: string
  label: string
  icon?: string
  iconPosition?: 'left' | 'right'
  loading?: boolean
}>()
</script>

<template>
  <component :is="tag" class="btn btn-primary" :disabled="loading">
    <div v-if="loading" class="spinner-border" role="status">
      <span class="visually-hidden">Loading...</span>
    </div>

    <i v-if="icon && 'left' === iconPosition" :class="`${icon} me-1`" />

    {{ label }}

    <i v-if="icon && 'right' === iconPosition" :class="`${icon} ms-1`" />
  </component>
</template>

<style scoped>
.spinner-border {
  width: 1rem;
  height: 1rem;
  margin-right: 0.5rem;
}
</style>
