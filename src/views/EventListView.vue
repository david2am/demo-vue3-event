<script setup>
import { ref, onMounted } from 'vue'
import EventService from '@/services/EventService'
import EventCard from '@/components/EventCard.vue'

const events = ref(null)

onMounted(async () => {
  try {
    const { data } = await EventService.getEvents()
    events.value = data
  } catch (error) {
    console.error(error)
  }
})
</script>

<template>
  <h1>Events For Good</h1>
  <div class="events">
    <EventCard v-for="event in events" :key="event.id" :event="event">
    </EventCard>
  </div>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
