<script setup lang="ts">
import { Database } from '~~/types/database.types'

const client = useSupabaseClient<Database>()

const { data: teams } = await useAsyncData('teams', async () => {
  const { data } = await client.from('teams').select('id, name').order('created_at')

  return data
})
</script>

<template>
  <ul v-if="teams">
    <li v-for="team in teams" :key="team.id">
      {{ team.name }}
    </li>
  </ul>
</template>
