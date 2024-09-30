<script setup>
import SectionCard from '@/components/SectionCard.vue'
import RoundButton from '@/components/RoundButton.vue'
import { LoaderCircle, Check } from 'lucide-vue-next'
import { computed } from 'vue'

// Define props with validation
const props = defineProps({
  title: String,
  status: {
    type: String,
    // Validate that status is either 'pending' or 'completed'
    validator: (value) => ['pending', 'completed'].includes(value)
  }
})

// Compute whether the booking is pending
const pending = computed(() => props.status === 'pending')

// Determine which icon to use based on the pending status
const icon = computed(() => (pending.value ? LoaderCircle : Check))

// Define emits for type checking and documentation
defineEmits(['cancelled'])
</script>

<template>
  <SectionCard>
    <div class="flex justify-between">
      <div class="flex space-x-2">
        <div>{{ title }}</div>
        <!-- Use dynamic component for icon, with conditional animation -->
        <div><component :is="icon" :class="{ 'animate-spin': pending }" /></div>
      </div>
      <!-- Emit 'cancelled' event when button is clicked -->
      <RoundButton variant="danger" @click="$emit('cancelled')">Cancel</RoundButton>
    </div>
  </SectionCard>
</template>

<!-- Remove empty style block if not needed -->
