<template>
  <div
    class="absolute bottom-0 left-0 right-0 bg-blue-400 flex focus-within:ring-yellow-800"
  >
    <input
      v-model="newMessage"
      type="text"
      class="flex-grow text-xl font-thin focus:outline-none"
      @change="send"
    />
    <button
      class="hover:bg-blue-600 rounded-sm px-8 focus:outline-none"
      @click="send"
    >
      <mdi:send />
    </button>
  </div>
</template>

<script setup>
import { ref } from "vue"
import { database } from "~/helpers/useFireBase"
const { sendMessage } = database()
const newMessage = ref(null)
const send = () => {
  if (newMessage.value?.length > 0) {
    sendMessage(newMessage.value)
    newMessage.value = null
  }
}
</script>
