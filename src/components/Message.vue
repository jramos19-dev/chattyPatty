<template>
  <div
    @click.stop="copyMessage"
    class="container mx-auto flex my-3 rounded-full transition transform cursor-pointer hover:scale-105"
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
  <div
    class="bg-yellow-300 fixed py-4 px-8 rounded-full bottom-16 right-4 z-10"
    v-if="copied"
  >
    <p>Message Copied!</p>
  </div>
</template>

<script setup>
import { defineProps, computed, ref } from "vue"
import { useClipboard } from "@vueuse/core"
import { authentication } from "~/helpers/useFireBase"
import { useMotions } from "@vueuse/motion"

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

const source = ref("")
const { copy, copied } = useClipboard({ source })

const copyMessage = () => {
  source.value = `${props.message.text} by ${props.message.userName}`
  copy()
}

const motions = useMotions()
</script>
