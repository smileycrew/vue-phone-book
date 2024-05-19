<script setup>
import { ref } from 'vue'
import sampleData from './sampleData'
import ContactForm from './components/ContactForm.vue'
import ContactList from './components/ContactList.vue'

const contactsInLocalStorage = JSON.parse(localStorage.getItem('contacts'))

const contacts = ref(contactsInLocalStorage || sampleData)

const addContactsToLocalStorage = () => {
  localStorage.setItem('contacts', JSON.stringify(contacts.value))
}

const addContact = (contact) => {
  contacts.value = [
    ...contacts.value,
    {
      id: Date.now(),
      ...contact
    }
  ]

  addContactsToLocalStorage()
}
const deleteContact = (contact) => {
  contacts.value = contacts.value.filter((c) => c.id !== contact.id)

  addContactsToLocalStorage()
}
</script>

<template>
  <h1 class="has-text-centered has-text-info is-size-1">Vue Phonebook</h1>

  <div class="container px-4">
    <div class="columns">
      <div class="column">
        <ContactForm @submit="addContact" />
      </div>

      <div class="column">
        <ContactList :contacts="contacts" @delete="deleteContact" />
      </div>
    </div>
  </div>
</template>

<style scoped></style>
