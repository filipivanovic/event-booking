<script setup>
import BookingItem from '@/components/BookingItem.vue'
import { onMounted } from 'vue'
import LoadingBookingItem from '@/components/LoadingBookingItem.vue'
import EventList from '@/components/EventList.vue'
import useBookings from '@/composable/useBookings.js'

const { bookings, loading, fetchBookings, cancelBooking } = useBookings()

onMounted(() => {
  fetchBookings()
})

</script>
<template>
  <main class="container mx-auto my-8 space-y-8">
    <h1 class="text-4xl font-medium">Event Booking App</h1>
    <h2 class="text-2xl font-medium">All Events</h2>
    <EventList />
    <h2 class="text-2xl font-medium">Your Bookings</h2>
    <section class="grid grid-cols-1 gap-4">
      <template v-if="!loading">
        <BookingItem v-for="booking in bookings"
                     :key="booking" :title="booking.eventTitle"
                     :status="booking.status"
                     @cancelled="cancelBooking(booking.id)"></BookingItem>
      </template>
      <template v-else>
        <LoadingBookingItem v-for="i in 4" :key="i"></LoadingBookingItem>
      </template>
    </section>
  </main>
</template>