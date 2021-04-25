<template>
  <Message v-for="(m, index) in messages" :key="index" :message="m" />
  <NewMessage />
</template>

<script setup>
import { database } from "~/helpers/useFireBase"
const { messages } = database()
</script>
