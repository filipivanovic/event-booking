<script setup>

import BookingItem from '@/components/BookingItem.vue'
import LoadingBookingItem from '@/components/LoadingBookingItem.vue'
import { onMounted } from 'vue'
import useBookings from '@/composable/useBookings.js'

const { bookings, loading, fetchBookings, cancelBooking } = useBookings()

onMounted(() => {
  fetchBookings()
})

</script>

<template>
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

<style scoped>

</style>