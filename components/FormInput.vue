<script setup lang="ts">
defineProps<{
  type: 'text' | 'password' | 'email'
  placeholder?: string
  label?: string
  icon?: string
}>()

const value = defineModel()
</script>

<template>
  <div class="input-group">
    <span v-if="icon" class="input-group-text">
      <i :class="icon" />
    </span>

    <div v-if="label" class="form-floating">
      <input
        :id="$.uid.toString()"
        v-model="value"
        :type="type"
        :placeholder="placeholder"
        class="form-control"
      >

      <label :for="$.uid.toString()">{{ label }}</label>
    </div>

    <input
      v-else
      v-model="value"
      :type="type"
      :placeholder="placeholder"
      class="form-control"
    >
  </div>
</template>
