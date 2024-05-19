<script setup>
import { computed } from 'vue'

const emit = defineEmits(['delete'])

const props = defineProps(['contact'])

const initials = computed(() => {
  const firstInitial = props.contact.firstName[0]
  const lastInitial = props.contact.lastName[0]

  return firstInitial + lastInitial
})
const fullName = computed(() => {
  return `${props.contact.firstName} ${props.contact.lastName}`
})

const handleRemoveContact = () => {
  emit('delete', props.contact)
}
</script>

<template>
  <div class="is-align-items-center is-flex py-1">
    <div class="has-background-info has-text-light initials mr-3">
      <div class="has-text-weight-bold">{{ initials }}</div>
    </div>

    <div class="is-flex-grow-1">
      <p class="is-size-5">{{ fullName }}</p>
      <div class="has-text-gray is-size-7">
        <span class="has-text-weight-semibold">Email:</span> {{ props.contact.email }}
      </div>

      <div class="has-text-gray is-size-7">
        <span class="has-text-weight-semibold">Phone:</span> {{ props.contact.phoneNumber }}
      </div>
    </div>

    <button class="button is-danger is-light is-small" @click="handleRemoveContact">Remove</button>
  </div>
</template>

<style scoped>
.initials {
  align-items: center;
  border-radius: 50%;
  display: flex;
  height: 3rem;
  justify-content: center;
  width: 3rem;
}
</style>
