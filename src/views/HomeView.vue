<template>
  <div>
    <h1>Users</h1>
    <div v-for="item in users" :key="item.id">
      <p>{{ item.name }}</p>
      <span>{{ item.id }}</span>
    </div>
  </div>
</template>

<script setup>
import gql from 'graphql-tag'
import { watchEffect, computed } from 'vue'
import { useQuery } from '@vue/apollo-composable'
const allUsersQuery = gql`
  query {
    users {
      id
      name
    }
  }
`

const { result } = useQuery(allUsersQuery)
// const users = useResult(result, [], result.users)

const users = computed(() => result.value?.users ?? [])

</script>