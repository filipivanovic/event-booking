<script setup>

import SectionCard from '@/components/SectionCard.vue'
import RoundButton from '@/components/RoundButton.vue'
</script>

<template>
  <SectionCard>
    <div class="flex justify-between">
      <slot></slot>
      <RoundButton variant="danger">Cancel</RoundButton>
    </div>
  </SectionCard>
</template>

<style scoped>

</style>