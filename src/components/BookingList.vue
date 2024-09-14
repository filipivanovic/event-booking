<script setup>

import BookingItem from '@/components/BookingItem.vue'
import LoadingBookingItem from '@/components/LoadingBookingItem.vue'
import { onMounted } from 'vue'
import useBookings from '@/composable/useBookings.js'
import ErrorCard from '@/components/ErrorCard.vue'

const { bookings, loading, fetchBookings, cancelBooking, error } = useBookings()

onMounted(() => {
  fetchBookings()
})

</script>

<template>
  <template v-if="error">
    <ErrorCard :retry="fetchBookings">
      Failed to fetch bookings.
    </ErrorCard>
  </template>
  <template v-else>
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
  </template>
</template>

<style scoped>

</style>