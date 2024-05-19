<script setup>
import { ref } from 'vue'

const emit = defineEmits(['search'])

const text = ref('')

const handleSearchContactList = () => {
  emit('search', text.value.toLowerCase())
}
</script>

<template>
  <div class="py-3">
    <input
      class="input"
      placeholder="Search contacts..."
      v-model="text"
      @input="handleSearchContactList"
    />
  </div>
</template>

<style scoped></style>
