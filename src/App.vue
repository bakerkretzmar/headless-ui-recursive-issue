<template>
  <Combobox v-model="selectedPerson">
    <ComboboxInput
      @change="query = $event.target.value"
      :displayValue="(person) => person.name"
    />
    <ComboboxOptions>
      <ComboboxOption
        v-if="query.length > 0"
        :value="{ id: null, name: query }"
      >
        Create "{{query}}"
      </ComboboxOption>
      <ComboboxOption
        v-for="person in filteredPeople"
        :key="person"
        :value="person"
      >
        {{ person.name }}
      </ComboboxOption>
    </ComboboxOptions>
  </Combobox>
</template>

<script setup>
  import { ref, computed } from 'vue'
  import {
    Combobox,
    ComboboxInput,
    ComboboxOptions,
    ComboboxOption,
  } from '@headlessui/vue'

  const people = [
    { id: 1, name: 'Durward Reynolds' },
    { id: 2, name: 'Kenton Towne' },
    { id: 3, name: 'Therese Wunsch' },
    { id: 4, name: 'Benedict Kessler' },
    { id: 5, name: 'Katelyn Rohan' },
  ]
  const selectedPerson = ref(people[0])
  const query = ref('')

  const filteredPeople = computed(() =>
    query.value === ''
      ? people
      : people.filter((person) => {
          return person.name.toLowerCase().includes(query.value.toLowerCase())
        })
  )
</script>
