<script setup lang="ts">
import { ref, toRefs } from 'vue'
import { type Event } from '@/types'
import { useRouter } from 'vue-router';

const props = defineProps<{
    event: Event
    id: String
}>()
// eslint-disable-next-line @typescript-eslint/no-unused-vars
const { event } = toRefs(props)
const router = useRouter()

const showMessage = ref(false)
const flashMessage = ref('')

const register = () => {
    // if the registration API call successful
    showMessage.value = true
    flashMessage.value = 'Registration successful!'
    setTimeout(() => {
        showMessage.value = false
        router.push({ name: 'event-detail-view' })
    }, 3000) // Adjust the timeout duration as needed
}
</script>

<template>
  <p>Register event here</p>
  <button @click="register">Register</button>
  <div v-if="showMessage" class="flash-message">
    {{ flashMessage }}
  </div>
</template>

<style scoped>
.flash-message {
  position: fixed;
  top: 20px;
  right: 20px;
  padding: 10px;
  background-color: #4caf50;
  color: white;
  border-radius: 5px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}
</style>
