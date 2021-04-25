<template>
  <div
    class="container mx-auto flex my-3 rounded-full"
    :class="isUser ? 'bg-amber-300' : 'bg-green-500'"
  >
    <div>
      <img
        class="rounded-full h-12"
        :src="message.userPhotoURL"
        :alt="`Avatar of ${message.userName}`"
      />
    </div>
    <div class="flex flex-grow text-xl bg-gray-500 rounded-xl">
      <div
        class="flex flex-grow items-center text-warmGray-200 justify-between px-8 rounded-full"
      >
        <p>{{ message.text }}</p>
        <p class="text-sm">{{ message.userName }}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { defineProps, computed, ref } from "vue"
import { authentication } from "~/helpers/useFireBase"

const { user } = authentication()

const isUser = computed(() => user.value.uid === props.message.userId)

const props = defineProps({
  message: {
    type: Object,
    default: () => ({
      userName: "",
      userId: "",
      userPhotoURL: "",
      text: "",
      createAt: "",
    }),
  },
})
</script>
