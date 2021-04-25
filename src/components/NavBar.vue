<template>
  <div
    class="fixed top-0 left-0 right-0 bg-gray-500 text-orange-700 py-6 text-xl z-10"
  >
    <div class="containter bg-yellow-300 flex justify-between items-center">
      <div class="brand flex space-x-2 text-3xl">
        <mdi:message-processing-outline class="text-orange-500" />
        <h1 class="text-gray-900 font-thin">
          Chatty<spa class="font-bold text-orange-600">Patty</spa>
        </h1>
      </div>

      <div class="menu">
        <div v-if="!isAuthenticated">
          <button
            class="text-coolGray-100 bg-gray-500 hover:bg-green-500 hover:text-gray-600 rounded-full"
            @click="googlePopup"
          >
            Sign In
          </button>
        </div>
        <div v-else class="flex items-center space-x-8">
          <p>Welcome {{ user?.displayName }}</p>
          <button
            class="text-coolGray-100 bg-orange-600 hover:bg-red-900 hover:text-warmGray-200 rounded-full"
            @click="signOut"
          >
            Sign Out
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { authentication } from "~/helpers/useFireBase"
const { isAuthenticated, user, googlePopup, signOut } = authentication()
</script>
