<script setup lang="ts">
import { Database } from '~~/types/database.types'

definePageMeta({
  middleware: 'auth'
})

const client = useSupabaseClient<Database>()

const { data: teams } = useAsyncData('teams', async () => {
  const { data } = await client
    .from('teams')
    .select('id, name')
    .order('created_at')

  return data
})
</script>

<template>
  <div>
    <div class="d-flex justify-content-between mb-4">
      <h1 class="mb-0">
        Teams
      </h1>

      <AppButton tag="button" label="Add team" />
    </div>

    <table v-if="teams && teams.length" class="table">
      <thead>
        <tr>
          <th scope="col">
            ID
          </th>

          <th scope="col">
            Name
          </th>

          <th scope="col">
            Actions
          </th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="team in teams" :key="team.id">
          <th scope="row">
            {{ team.id }}
          </th>

          <td>{{ team.name }}</td>

          <td>edit del</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
