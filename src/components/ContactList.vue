<script setup>
import { computed, ref } from 'vue'
import ContactListItem from './ContactListItem.vue'
import SearchForm from './SearchForm.vue'
import EmptyList from './EmptyList.vue'

const searchText = ref('')

const emit = defineEmits(['delete'])

const props = defineProps(['contacts'])

const handleDeleteContact = (contact) => {
  emit('delete', contact)
}
const changeSearchText = (text) => {
  searchText.value = text
}

const computedContacts = computed(() => {
  return props.contacts.filter((contact) =>
    contact.firstName.toLowerCase().includes(searchText.value)
  )
})
</script>

<template>
  <SearchForm @search="changeSearchText" />

  <div class="panel is-success">
    <div class="panel-heading">Contacts</div>
    <div
      class="is-align-items-stretch is-flex is-flex-direction-column panel-block"
      v-if="computedContacts.length > 0"
    >
      <div :key="contact.phoneNumber" v-for="contact in computedContacts">
        <ContactListItem :contact="contact" @delete="handleDeleteContact" />
      </div>
    </div>

    <div class="is-align-items-stretch is-flex is-justify-content-center py-5" v-else>
      <EmptyList />
    </div>
  </div>
</template>

<style scoped></style>
