<template>
  <Notification bottom right v-model="show">
    <template #icon>
      <svg class="h-6 w-6 text-gray-400" fill="currentColor" viewBox="0 0 20 20">
        <path fill-rule="evenodd" d="M8.257 3.099c.765-1.36 2.722-1.36 3.486 0l5.58 9.92c.75 1.334-.213 2.98-1.742 2.98H4.42c-1.53 0-2.493-1.646-1.743-2.98l5.58-9.92zM11 13a1 1 0 11-2 0 1 1 0 012 0zm-1-8a1 1 0 00-1 1v3a1 1 0 002 0V6a1 1 0 00-1-1z" clip-rule="evenodd"/>
      </svg>
    </template>
    <template #title>
      Connection lost
    </template>
    <template #actions>
      <button
        class="text-sm leading-5 font-medium text-indigo-600 hover:text-indigo-500 focus:outline-none focus:underline transition ease-in-out duration-150"
        @click="reloadPage"
      >
        Reload
      </button>
    </template>

    This page may display outdated information due to connection issues.
  </Notification>
</template>

<script>
  import { mapGetters } from 'vuex'
  import Notification from 'ui/notifications/Notification'

  export default {
    name: 'SseConnectionErrorNotification',
    components: { Notification },
    data() {
      return {
        show: false,
      }
    },
    computed: mapGetters('streams', ['hasSseError']),
    watch: {
      hasSseError: {
        handler(val) {
          if (val) {
            this.show = true
          }
        },
        immediate: true,
      },
    },
    methods: {
      reloadPage() {
        location.reload()
      },
    },
  }
</script>
