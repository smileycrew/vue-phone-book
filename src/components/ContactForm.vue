<script setup>
import { computed, ref } from 'vue'
// emitters
const emit = defineEmits(['submit'])

// refs
const form = ref({
  email: '',
  firstName: '',
  lastName: '',
  phoneNumber: ''
})

// computed values
const formIsValid = computed(() => {
  return Boolean(
    form.value.email && form.value.firstName && form.value.lastName && form.value.phoneNumber
  )
})
const computedPhoneNumber = computed(() => {
  const areaCode = form.value.phoneNumber.slice(0, 3)
  const prefix = form.value.phoneNumber.slice(3, 6)
  const extention = form.value.phoneNumber.slice(5, 9)

  return `(${areaCode})-${prefix}-${extention}`
})

// handlers
const handleSubmit = () => {
  console.log(computedPhoneNumber)
  emit('submit', {
    ...form.value,
    phoneNumber: computedPhoneNumber.value
  })

  form.value = {
    email: '',
    firstName: '',
    lastName: '',
    phoneNumber: ''
  }
}
</script>

<template>
  <div class="is-success panel">
    <div class="panel-heading">Add Contact</div>

    <div class="panel-block">
      <form
        class="is-flex is-flex-direction-column is-flex-grow-1 mt-3"
        @submit.prevent="handleSubmit"
      >
        <div class="field">
          <label class="label">Email</label>

          <div class="control">
            <input
              class="input"
              :class="{ 'is-danger': !form.email }"
              placeholder="Email"
              type="text"
              v-model="form.email"
            />
            <p class="help is-danger" v-if="!form.email">Email is required</p>
          </div>
        </div>

        <div class="field">
          <label class="label">First Name</label>

          <div class="control">
            <input
              class="input"
              :class="{ 'is-danger': !form.firstName }"
              placeholder="First name..."
              type="text"
              v-model="form.firstName"
            />
            <p class="help is-danger" v-if="!form.firstName">First name is required</p>
          </div>
        </div>

        <div class="field">
          <label class="label">Last Name</label>

          <div class="control">
            <input
              class="input"
              :class="{ 'is-danger': !form.lastName }"
              placeholder="Last name..."
              type="text"
              v-model="form.lastName"
            />
            <p class="help is-danger" v-if="!form.lastName">Last name is required</p>
          </div>
        </div>

        <div class="field">
          <label class="label">Phone Number</label>

          <div class="control">
            <input
              class="input"
              :class="{ 'is-danger': !form.phoneNumber }"
              maxlength="10"
              placeholder="Phone number..."
              type="text"
              v-model="form.phoneNumber"
            />
            <p class="help is-danger" v-if="!form.phoneNumber">Phone number is required</p>
          </div>
        </div>

        <button class="button is-info is-link" :disabled="!formIsValid" type="submit">
          Add contact
        </button>
      </form>
    </div>
  </div>
</template>

<style scoped></style>
