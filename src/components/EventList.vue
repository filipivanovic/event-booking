<script setup>
// Import necessary components
import EventCard from '@/components/EventCard.vue'
import LoadingEventCard from '@/components/LoadingEventCard.vue'
import ErrorCard from '@/components/ErrorCard.vue'

import { ref, onMounted } from 'vue'
// Import custom composable for handling bookings
import useBookings from '@/composable/useBookings.js'

// Reactive references for managing component state
const events = ref([]) // Stores the list of events
const loading = ref(false) // Tracks loading state
const error = ref(null) // Stores any error that occurs

// Extract handleRegistration function from the useBookings composable
const { handleRegistration } = useBookings()

// Function to fetch events from the API
const fetchEvents = async () => {
  loading.value = true
  error.value = null
  try {
    const response = await fetch('http://localhost:3001/events')
    events.value = await response.json()
  } catch (e) {
    error.value = e
  } finally {
    loading.value = false
  }
}

// Fetch events when the component is mounted
onMounted(() => {
  fetchEvents()
})
</script>

<template>
  <template v-if="error">
    <!-- Display error message if an error occurred -->
    <ErrorCard :retry="fetchEvents">
      Could not load events at the moment. Please try again.
    </ErrorCard>
  </template>
  <template v-else>
    <section class="grid grid-cols-1 desktop:grid-cols-2 gap-8">
      <template v-if="!loading">
        <template v-if="events.length">
          <EventCard
            v-for="event in events"
            :key="event.id"
            :title="event.title"
            :when="event.date"
            :description="event.description"
            @register="handleRegistration(event)"
          />
        </template>
        <template v-else>
          <div class="col-span-2 text-center text-gray-500">No events yet.</div>
        </template>
      </template>
      <template v-else>
        <LoadingEventCard v-for="i in 4" :key="i"></LoadingEventCard>
      </template>
    </section>
  </template>
</template>

<style scoped></style>
