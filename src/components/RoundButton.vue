
<script setup>

const variants = {
  default: 'border border-gray-200 hover:bg-gray-100',
  danger: 'bg-red-200 enabled:hover:bg-red-100 text-red-900'
}

defineEmits(['click'])
defineProps({
  variant: {
    type: String,
    default: 'default'
  }
})

</script>

<template>
  <button :class="['text-sm font-medium rounded-full px-3 py-1 hover:bg-gray-100', variants[variant] ?? variants.default]" @click="$emit('click')">
    <slot></slot>
  </button>
</template>

<style scoped>

</style>